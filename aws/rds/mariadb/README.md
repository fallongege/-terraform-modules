# aws/rds/mariadb - Relational Database Service - MariaDB
This module is used to create an RDS instance.

## What this does

 - Create RDS instance named after `db_name`

## Required Inputs

 - `tag_app_name` - Name of application, ex: Doorman, IdP, etc.
 - `tag_app_env` - Name of environment, ex: production, testing, etc.
 - `db_name` - Name of database to be created by default
 - `db_root_user` - Root database username
 - `db_root_pass` - Root database account password
 - `subnet_group_name` - Name of DB subnet group to place instance in
 - `availability_zone` - Availability zone name to place instance in
 - `security_groups` - List of security group ids to assign instance to

### Optional Inputs

 - `engine` - Default: `mariadb`
 - `engine_version` - Default: `<empty>`
 - `allocated_storage` - Default: `8`G
 - `storage_type` - Default: `gp2`
 - `instance_class` - Default: `db.t2.micro`
 - `backup_retention_period` - Default: `14` days
 - `multi_az` - Default: `false`

## Outputs

 - `id` - RDS instance ID
 - `arn` - ARN of RDS instance ID
 - `address` - Address for RDS instance
 - `port` - Port for RDS instance
 - `endpoint` - Full address+port of RDS instance

## Example Usage

```hcl
module "rds" {
  source = "github.com/silinternational/terraform-modules//aws/rds/mariadb"
  tag_app_name = "${var.tag_app_name}"
  tag_app_env = "${var.tag_app_env}"
  db_name = "${var.db_name}"
  db_root_user = "${var.db_root_user}"
  db_root_pass = "${var.db_root_pass}"
  subnet_group_name = "${module.vpc.db_subnet_group_name}"
  availability_zone = "${var.aws_zones[0]}"
  security_groups = ["${module.vpc.vpc_default_sg_id}"]
}
```