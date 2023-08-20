provider "aws" {
  region  = "ap-south-1"
}

terraform {
  backend "s3" {
      bucket = "ppterraformstate"
      key    = "build/terraform.tfstate"
      region = "ap-south-1"
  }
}

data "aws_iam_policy_document" "website_policy" {
  statement {
    actions = [
      "s3:GetObject"
    ]
    principals {
      identifiers = ["*"]
      type = "AWS"
    }
    resources = [
      "arn:aws:s3:::ppwebsitestorage/*"
    ]
  }
}

resource "aws_s3_bucket" "s3Bucket" {
     bucket = "ppwebsitestorage"
     acl       = "public-read"

     policy = data.aws_iam_policy_document.website_policy.json

   website {
       index_document = "index.html"
   }
}
