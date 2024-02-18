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
<script src="https://gist.github.com/dedunumax/6073737d6d790a457bbe89627c723ede.js"></script>

### Tags

- aws
- backup
- terraform
