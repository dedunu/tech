---
layout: post
title: "Private S3 bucket and CloudFront with Terraform"
---

I wanted to setup a CDN for [my travel blog](https://dedunu.click). I followed couple of resources and came up with this setup.

`terraform.tf`
```terraform
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "5.8.0"
    }
  }
}
```

`variables.tf`
```terraform
variable "cdn1_domain_name" {
  default = "cdn1.dedunu.click"
}

variable "root_domain_name" {
  default = "dedunu.click"
}
```

`provider.tf`
```terraform
provider "aws" {
  region = "us-east-1"
}
```

`data.tf`
```terraform
data "aws_route53_zone" "default" {
  name = "dedunu.click"
}
```

`s3.tf`
```terraform
resource "aws_s3_bucket" "default" {
  bucket = var.cdn1_domain_name
}

resource "aws_s3_bucket_website_configuration" "default" {
  bucket = aws_s3_bucket.default.id

  index_document {
    suffix = "index.html"
  }

  error_document {
    key = "index.html"
  }
}

resource "aws_s3_bucket_ownership_controls" "default" {
  bucket = aws_s3_bucket.default.id
  rule {
    object_ownership = "BucketOwnerPreferred"
  }
}

resource "aws_s3_bucket_public_access_block" "default" {
  bucket = aws_s3_bucket.default.id

  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}

resource "aws_s3_bucket_acl" "default" {
  depends_on = [
    aws_s3_bucket_ownership_controls.default,
    aws_s3_bucket_public_access_block.default,
  ]

  bucket = aws_s3_bucket.default.id
  acl    = "private"
}

resource "aws_s3_bucket_policy" "default" {
  bucket = aws_s3_bucket.default.id
  policy = data.aws_iam_policy_document.default.json
}

data "aws_iam_policy_document" "default" {
  statement {
    sid = "1"

    principals {
      type        = "Service"
      identifiers = ["cloudfront.amazonaws.com"]
    }

    actions = [
      "s3:GetObject",
    ]

    resources = [
      "arn:aws:s3:::${var.cdn1_domain_name}/*"
    ]

    condition {
      test     = "StringEquals"
      variable = "AWS:SourceArn"
      values = [
        aws_cloudfront_distribution.default.arn
      ]
    }
  }

}
```

`cloudfront.tf`
```terraform
resource "aws_cloudfront_distribution" "default" {

  origin {
    domain_name              = aws_s3_bucket.default.bucket_regional_domain_name
    origin_id                = var.cdn1_domain_name
    origin_access_control_id = aws_cloudfront_origin_access_control.default.id
  }

  enabled             = true
  default_root_object = "index.html"

  default_cache_behavior {
    viewer_protocol_policy = "redirect-to-https"
    compress               = true
    allowed_methods        = ["GET", "HEAD"]
    cached_methods         = ["GET", "HEAD"]
    target_origin_id       = var.cdn1_domain_name
    min_ttl                = 0
    default_ttl            = 86400
    max_ttl                = 31536000

    forwarded_values {
      query_string = false
      cookies {
        forward = "none"
      }
    }
  }

  aliases = ["${var.cdn1_domain_name}"]

  restrictions {
    geo_restriction {
      restriction_type = "none"
    }
  }

  viewer_certificate {
    acm_certificate_arn = aws_acm_certificate.default.arn
    ssl_support_method  = "sni-only"
  }
}

resource "aws_cloudfront_origin_access_control" "default" {
  name                              = "cdn1_dedunu_click_oac"
  origin_access_control_origin_type = "s3"
  signing_behavior                  = "always"
  signing_protocol                  = "sigv4"
}
```

`acm.tf`
```terraform
resource "aws_acm_certificate" "default" {
  domain_name               = "*.${var.root_domain_name}"
  validation_method         = "EMAIL"
  subject_alternative_names = ["${var.root_domain_name}"]
}
```

`route53.tf`
```terraform
resource "aws_route53_record" "default" {
  zone_id = data.aws_route53_zone.default.zone_id
  name    = var.cdn1_domain_name
  type    = "A"

  alias {
    name                   = aws_cloudfront_distribution.default.domain_name
    zone_id                = aws_cloudfront_distribution.default.hosted_zone_id
    evaluate_target_health = false
  }
}
```

Finally I synced files with this command.

```bash
aws s3 sync . s3://cdn1.dedunu.click
```

### References

- <https://medium.com/runatlantis/hosting-our-static-site-over-ssl-with-s3-acm-cloudfront-and-terraform-513b799aec0f>
- <https://awstip.com/aws-cloudfront-with-s3-as-origin-using-terraform-a369cdadc541>

### Tags

- terraform
- aws
- s3
- cloudfront
- private s3
