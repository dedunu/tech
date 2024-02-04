---
layout: post
title: "Terraform: AWS Backup Policies"
---

This is an example how to enforce AWS backup with Organizational Backup Policies. Users on sub-accounts cannot edit these rules. You can ensure that these policies are not changed anywhere else other than the organizational policy section. You have to create these on the root account.

`provider.tf`

```hcl
﻿﻿provider "aws" {
  region  = "us-east-1"
}
```

`backend.tf`
```hcl
terraform {
  required_version = ">= 1.6.1"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}
```

`organizational_policy.tf`
```hcl
resource "aws_organizations_policy" "plan_1_policy" {
  name = "dedunu-info-backup-plan-1-policy"
  type = "BACKUP_POLICY"

  content = jsonencode(local.plan1)
}

resource "aws_organizations_policy_attachment" "plan_1_policy_attachment" {
  policy_id = aws_organizations_policy.plan_1_policy.id
  target_id = "<account-id>"
}

locals {
  plan1 = {
    "plans" : {
      "dedunu-info-backup-plan-1" : {
        "regions" : {
          "@@assign" : [
            "us-east-1",
            "us-east-2"
          ]
        },
        "rules" : {
          "dedunu-info-backup-plan-1-rule" : {
            "schedule_expression" : { "@@assign" : "cron(0 5 ? * * *)" },
            "target_backup_vault_name" : { "@@assign" : "aws-backup-vault" },
            "start_backup_window_minutes" : { "@@assign" : "60" },
            "complete_backup_window_minutes" : { "@@assign" : "180" },
            "enable_continuous_backup" : { "@@assign" : "false" },
            "lifecycle" : {
              "delete_after_days" : { "@@assign" : "14" }
            },
            "recovery_point_tags" : {
              "Owner" : {
                "tag_key" : { "@@assign" : "cost-center" },
                "tag_value" : { "@@assign" : "longterm-backup" }
              }
            },
          }
        },
        "selections" : {
          "tags" : {
            "dedunu-info-backup-plan-1-selection" : {
              "iam_role_arn" : { "@@assign" : "arn:aws:iam::$account:role/service-role/AWSBackupDefaultServiceRole" },
              "tag_key" : { "@@assign" : "backup" },
              "tag_value" : { "@@assign" : ["dedunu-backup-daily-plan-1"] }
            }
          }
        }
      }
      }
  }
}
```

### Tags

- aws
- backup
- terraform
