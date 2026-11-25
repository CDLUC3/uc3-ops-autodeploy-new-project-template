UC3 Autodeploy New Project Template
===================================

Each uc3 service team must have complete control over respective build/deploy stacks.
But I want to centralize tamplates and documentation in a shared repo.


repos
-----
```
uc3-ops-autodeploy
uc3-ops-autodeploy-new-project-template
```

active projects
---------------
```
dmp-autodeploy
ezid-autodeploy
uc3-ops-logstash-autodeploy
ngrams-autodeploy
```

project layout
--------------
```
.
├── README.md
├── config
│   ├── config.yaml
│   └── dev
│       ├── config.yaml
│       ├── logstash
│       │   ├── codebuild.yaml
│       │   ├── codepipeline.yaml
│       │   ├── config.yaml
│       │   ├── ecr.yaml
│       │   └── lambda.yaml
│       └── prereqs.yaml
└── subtree
    ├── README.md
    ├── docs
    │   ├── auto_build_workflow_diagram.md
    │   ├── auto_deploy_workflow_diagram.md
    │   ├── buildspec.yaml.sample
    │   └── image_tag_timeline.md
    ├── notes
    ├── reference_config
    │   ├── config.yaml
    │   └── dev
    │       ├── config.yaml
    │       ├── logstash
    │       │   ├── codebuild.yaml
    │       │   ├── codepipeline.yaml
    │       │   ├── config.yaml
    │       │   ├── ecr.yaml
    │       │   └── lambda.yaml
    │       └── prereqs.yaml
    └── templates
        ├── codebuild.yaml.j2
        ├── codepipeline.yaml.j2
        ├── data
        │   └── lambda
        │       └── ecs_autodeploy.py
        ├── ecr.yaml
        ├── lambda.yaml.j2
        └── prereqs.yaml.j2
```


Setup
-----


1. Create your new autodeploy project repository from github template.

   Follow instruction for [Creating a Repository from a Template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template#creating-a-repository-from-a-template).
   
   For **owner** select `CDLUC3`.
   
   Set access rights for devs on your team.

1. Clone your new repo onto your workstation.

   Examples based on `ngrams-autodeploy`
   ```
   git clone git@github.com:CDLUC3/ngrams-autodeploy.git
   cd ngrams-autodeploy/
   ```

1. Set up subtree 
   ```
   git remote add autodeploy-subtree git@github.com:CDLUC3/uc3-ops-autodeploy.git
   git subtree add --prefix subtree autodeploy-subtree main --squash
   ```

1. Set up symlinks for `templates` and `docs`
   ```
   ln -s subtree/templates/ templates 
   ln -s subtree/docs/ docs 
   ```

1. Initialize your sceptre config.

   Copy contents of `subtree/reference_config` into `config/` directory of your new autobuild project:
   ```
   cp -a subtree/reference_config config
   mv config/dev/logstash config/dev/<my-app>
   ```
   Edit stack configs and `sceptre_user_data` approprate to your own ECS services.

1. Validate your project configuration
   ```
   sceptre generate dev/prereqs.yaml
   sceptre generate dev/<my-app>/ecr.yaml
   sceptre generate dev/<my-app>/codebuild.yaml
   sceptre generate dev/<my-app>/codepipeline.yaml
   sceptre generate dev/<my-app>/lambda.yaml
   ```



`git subtree` Usage
-------------------
Links:
- https://www.datacamp.com/tutorial/git-subtree
- https://git-memo.readthedocs.io/en/latest/subtree.html


### Update your subtree
```
git subtree pull --prefix subtree autodeploy-subtree main --squash
```

Pull in subtree updates from an alternate branch
```
git subtree pull --prefix subtree autodeploy-subtree my-feature-branch --squash
```


### Update remote subtree repo

1. push to a topic branch on remote
   ```
   git subtree push --prefix=subtree autodeploy-subtree revise_lambda
   ```

1. create pull request on remote

1. after PR is merged on remote, be sure to sync your local subtree with remote to capture any modifications.


example output
```
agould@Linux:~/git/github/cdluc3/uc3-ops-logstash-autodeploy> git subtree push --prefix=subtree autodeploy-subtree revise_lambda
git push using:  autodeploy-subtree revise_lambda
Enumerating objects: 76, done.
Counting objects: 100% (76/76), done.
Delta compression using up to 18 threads
Compressing objects: 100% (59/59), done.
Writing objects: 100% (67/67), 7.72 KiB | 2.57 MiB/s, done.
Total 67 (delta 31), reused 3 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (31/31), completed with 6 local objects.
remote: 
remote: Create a pull request for 'revise_lambda' on GitHub by visiting:
remote:      https://github.com/CDLUC3/uc3-ops-autodeploy/pull/new/revise_lambda
remote: 
To github.com:CDLUC3/uc3-ops-autodeploy.git
 * [new branch]      467169e8424b66518e958ed78caba35932a456ba -> revise_lambda
```









ToDo
----

DONE explore using github template repository feature:
