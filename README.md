UC3 Ops Autodeploy New Project Template
=======================================

Each uc3 service team must have complete control over respective build/deploy stacks.
But I want to centralize tamplates and documentation in a shared repo.


repos
-----
uc3-ops-autodeploy-new-project-template
uc3-ops-autodeploy-subtree

active projects
---------------
dmp-autodeploy
ezid-autodeploy
ops-autodeploy
ngrams-autodeploy

project layout
--------------
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
    │       ├── demoapp
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


Setup
-----

~> cd ~/git-repos/
~/git-repos> 






Notes
-----
### git subtree usage
Links:
- https://www.datacamp.com/tutorial/git-subtree
- https://git-memo.readthedocs.io/en/latest/subtree.html
