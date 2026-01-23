# Changes from Original Lesson-14

## Version Updates

### Terraform
- **Old:** `>= 1.4.6`
- **New:** `>= 1.14.0`

### AWS Provider
- **Old:** `5.01`
- **New:** `~> 6.26`

### Azure Provider
- **Old:** `=3.0.0`
- **New:** `~> 4.0`

### S3 Bucket Module
- **Old:** `3.14.0`
- **New:** `4.2.2`

## Configuration Changes

### bucket/main.tf
1. Updated AWS provider version to `~> 6.26`
2. Updated Terraform version to `>= 1.14.0`
3. Updated S3 module from `3.14.0` to `4.2.2`
4. **Removed** `acl = "private"` (deprecated in newer module)
5. Changed `object_ownership` to `"BucketOwnerEnforced"` (recommended setting)

### instances/version.tf
1. Updated AWS provider from `5.01` to `~> 6.26`
2. Updated Azure provider from `=3.0.0` to `~> 4.0`
3. Updated Terraform version to `>= 1.14.0`

## Compatibility Notes

- All resources tested and working with AWS provider 6.26
- S3 bucket module 4.x removes ACL in favor of object ownership settings
- Azure provider 4.x maintains compatibility with existing resources
- No changes needed to:
  - EC2 instances
  - Security groups
  - IAM users
  - Random resources
  - Ansible configuration
  - Bash scripts

## Breaking Changes Fixed

### S3 Module
The `acl` parameter was deprecated in the S3 module. The new configuration uses:
```hcl
control_object_ownership = true
object_ownership         = "BucketOwnerEnforced"
```

This is the AWS-recommended setting for new buckets and provides better security.

## Testing Status

✅ All configurations validated with `terraform validate`
✅ Compatible with Terraform 1.14.2
✅ Compatible with AWS Provider 6.26
✅ S3 module 4.2.2 tested and working

## Migration Notes

If upgrading from the old version:
1. Run `terraform destroy` on old infrastructure first
2. Update all `.tf` files with new versions
3. Run `terraform init -upgrade` to get new provider versions
4. Proceed with normal `terraform apply`

The state file format is compatible, but it's recommended to start fresh due to the S3 module changes.
