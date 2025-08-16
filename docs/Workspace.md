Terraform Workspace
===================

A Terraform workspace is a way for Terraform to manage multiple state files within the same configuration.

Normally, Terraform keeps track of infrastructure using a state file (terraform.tfstate). If you run the same configuration multiple times, Terraform will always apply changes to the same infrastructure defined in that state. Workspaces allow you to separate those states while still reusing the same code.

## 1. Default workspace
Every Terraform project starts with a default workspace.

If not specified, it will always use this workspace.

## 2. Create a new workspace
```bash
terraform workspace new <name>
terraform workspace new dev
terraform workspace new prod
```

Each of these workspaces will have its own state file, so resources created in dev won’t interfere with those in prod.

## 3. Switching workspace
```bash
terraform workspace select dev
```

## 4. State location
+ Local: `terraform.tfstate.d/<workspace_name>/terraform.tfstate`
+ Remote: A state file for each workspace.

## 5. Workspace name in config
You can refer the workspace name in code using workspace variable:
```hcl
resource "aws_s3_bucket" "example" {
  bucket = "my-bucket-${terraform.workspace}"
}
```
