# tg-aws-module-skeleton

This repository contains bare minimum code necessary to generate the terragrunt configuration for deploying `s3-bucket` to aws cloud platform.

This repository is intended to be used by developers wanting to write terragrunt configurations to deploy the terraform modules to `aws cloud platform`.

The terragrunt configurations(once fully generated) provide s3 bucket where remote state will be stored by terraform, provide configuration, and DRY terragrunt code to deploy the terraform modules.

# How to use this repository

1. Clone this repository on local workstation.
2. Make changes to `skeleton.yaml` file specific to your project/configurations.
3. Run make target `make configure`
4. Run make target `make terragrunt/generate`

Steps above should create terragrunt configurations that will be used in conjuction with configurations provided via `properties` repository (to supply variables to terraform code for each environment/instance).

# skeleton.yaml schema and content

This is sample schema of the `skeleton.yaml` file

```
naming_prefix: <<naming prefix to be used for deployed resources>>
module_file_name: <<file name with .hcl extention that will reside under common folder>>
git_repo_url: <<http git url of the terraform module to be deployed>>
envs:
  - <<environment name>>:
      regions:
        - <<region_1>>:
            instances:
              - "<<instance number>>"
      profile: <<aws profile used for authentication to connect to aws platform>>
```

`skeleton.yaml`(located at the root of the repository) is example file that generates terragrunt configurations for `dev`, `qa`, `uat`, `prod` environments, one instance each ("000") in `us-east-2` region. The terragrunt configuration is generated to deploy `s3 bucket` using wrapper module `tf-aws-wrapper_module-s3_bucket` and naming_prefix `demo-101`.
