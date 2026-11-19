UC3 Autodeploy New Project Template
===================================

Each uc3 service team must have complete control over respective build/deploy stacks.
But I want to centralize tamplates and documentation in a shared repo.


repos
-----
```
uc3-ops-autodeploy-new-project-template
uc3-ops-autodeploy-subtree
```

active projects
---------------
```
dmp-autodeploy
ezid-autodeploy
uc3-ops-autodeploy
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


1. Create your autodeploy project repository from github template

1. Set up subtree
   ```
   git remote add autodeploy-subtree git@github.com:CDLUC3/uc3-ops-autodeploy-subtree.git
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















Example based on EZID

In github create a new private repository `ezid-autodeploy`.  Do not add
README.md, .gitignore, or licence.  Set access rights for devs on your team.

```
~> cd ~/git-repos/
~/git-repos> git clone https://github.com/CDLUC3/uc3-ops-autodeploy-new-project-template ezid-autodeploy
~/git-repos> cd ezid-autodeploy/
~/git-repos/ezid-autodeploy> git remote set-url origin git@github.com:CDLUC3/ezid-autodeploy.git
~/git-repos/ezid-autodeploy> git push --set-upstream origin main

~/git-repos/ezid-autodeploy> git remote add autodeploy-subtree git@github.com:CDLUC3/uc3-ops-autodeploy-subtree.git
~/git-repos/ezid-autodeploy> git subtree add --prefix subtree autodeploy-subtree main --squash



Set up your sceptre config based on `subtree/reference_config`
```
~/git-repos/ezid-autodeploy> cp -a subtree/reference_config config
```




Updating your subtree
---------------------

```
~/git-repos/ezid-autodeploy> git subtree pull --prefix subtree autodeploy-subtree main --squash

ops-autodeploy> git subtree pull --prefix subtree autodeploy-subtree git-subtree --squash
```



Notes
-----
### git subtree usage
Links:
- https://www.datacamp.com/tutorial/git-subtree
- https://git-memo.readthedocs.io/en/latest/subtree.html




ToDo
----

explore using github template repository feature:
  https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template
