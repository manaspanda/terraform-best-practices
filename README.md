# Terraform Best Practices

## Table of Contents

- [What is Terraform](#what-is-terraform)
- [Terraform Best Practices](#terraform-best-practices)
  - [Remote backend to save state](#remote-backend-to-save-state)
  - [Separate environments with var-file](#separate-environments-with-var-file)
  - [Share state with remote backend](#Share-state-with-remote-backend)
  - [Validate and format Terraform code](#validate-and-format-terraform-code)
  - [Always tag resources](#always-tag-resources)
  - [Create reusable and composable modules](#create-reusable-and-composable-modules)
  - [Smaller de-coupled deployments](#smaller-de-coupled-deployments)
  - [Check execution plan before apply](#check-execution-plan-before-apply)
- [What is Terraform Module](#what-is-terraform-module)
- [Terraform Module Best Practices](#terraform-module-best-practices)

## What is Terraform

[Terraform](https://www.terraform.io) is a tool for building, changing, and versioning infrastructure safely and efficiently. Terraform provides many features including:
* Infrastructure as Code: High-level syntax (HCL), change management 
* Execution Plan: Plan and predict changes
* Resource Graph: Parallel and serial execution
* Change Automation: Complex changeset, clone deployments

## What is Terraform Module

### Remote backend to save state
Terraform saves the infrastructure deployment state in terraform state files. Save the terraform state files in remote backend, such as S3.
* Remote state is protected with locks that prevent corruption
* Stored only in memory; sensitive information is kept on backend

### Separate environments with var-file
Keep the terraform code for various environments (dev, stage, prod) common, and separate environment specific variables in var files.
* Reduces amount of code duplication
* Store all variables in a .tfvars file (eg. stage.tfvars, prod.tfvars)
* Load env variables at runtime

### Share state with remote backend
Once resources have been created in remote state, it can be referenced from other depoyments using remote backend or data-sources.

### Validate and format Terraform code
Terraform has formatting and validation options.

`terraform validate` - validates syntax on terraform files in the directory
`terraform fmt` - rewrites terraform files in proper format/style
`tflint` can be used to validate provider specific issues

### Always tag resources
Add appropriate tags to track your deployment assets. Create a convention to tag the asset, such as 
`environment`, `application`, `owner-name`, `owner-email`

### Create reusable and composable modules
Package infrastructure code into reusable and composable modules.

### Smaller de-coupled deployments
Its always easier to manage smaller de-coupled deployments, instead of a big deployment with different kinds of resources.

### Check execution plan before apply
Always review the plan with team, before applying the infrastructure changes.

## What is Terraform Module

[Terraform Module](https://www.terraform.io/docs/modules/) are re-usable and composible blueprint for your infrastructure solutions.
* Architecture and Solution abstraction: Apps and Database
* Reusable library for Infrastructure
* Compose modules to build end-to-end stack
* Lots of open-source on [Terraform registry](https://registry.terraform.io)

## Terraform Module Best Practices
Following are some of the best practices to create good terraform modules:

* Create meaningful abstractions
* Recommended module repo name: terraform-<provider>-<name>
* Follow standard module structure
* Semantically version (x.y.z) modules: git tags
* Include usage examples
* Good README
