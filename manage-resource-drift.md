Changes performed outside of Terraform over resources, usually will get the terraform state out of sync. 
When Terraforms detects the differences between your configuration and the actual resources, Terraform will attempt to reconcile your infrastructure, 
which may unintentionally destroy or recreate resources. 
A way to fix the previos scenario is:
- Run `terraform plan -refresh-only` to determine the drift between your current state file and actual configuration.
- `terraform apply -refresh-only` to Apply these changes to make your state file match your real infrastructure, but not your Terraform configuration
- Add the missing configuration to your configuration files
- Import the externally added resources to your state:  `terraform import provider_resource_type.resource_name resource_id`
- Check the imported resources in you terraform state: `terraform state list`
- Update your resources: `terraform apply`
