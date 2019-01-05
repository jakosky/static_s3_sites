# Why static_s3_sites?
* You want subdomains dev, tst, and www of a given domain name.
* You want to log access to both CloudFront and S3. Logs will be placed in an S3 bucket.
* You do not want to allow public access to your S3 buckets except through CloudFront.

# CloudFormation Template Inputs
## DomainName:
  Description: The DNS name of an existing Amazon Route 53 hosted zone e.g. jevsejev.io
## LoggingBucket:
  Description: The name of an existing S3 bucket to receive logs of activity in other S3 buckets.
## OriginAccessIdentity:
  Description: The ID (not canonical) of the Origin Access Identity.
## OriginAccessIdentityCanonicalId:
  Description: The Amazon S3 canonical user ID of an existing Origin Access Identity.
## AcmCertificateArn:
  Description: the Amazon Resource Name (ARN) of an AWS Certificate Manager (ACM) certificate.

# Overview of Template Actions
* Create buckets for dev.domain.name, tst.domain.name, www.domain.name and domain.name.
* Add Origin Access Identity to S3 buckets.
* Block public access to buckets except through CloudFront. Except for domain.name, because we need to leverage redirection offered only to S3 Website Endpoints.
* Create CloudFront distribution for each bucket.
* Add ACM Certificate to all CloudFront distributions.
* Set domain.name to route requests to https://www.domain.name.
