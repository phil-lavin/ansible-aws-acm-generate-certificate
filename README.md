Ansible playbook to generate or get a certificate from AWS Amazon Certificate Manager (ACM)

## Requirements

* It assumes the Route53 zone for your domain exists in the current AWS account
* Requires community.aws (ansible-galaxy collection install community.aws). This is for Route53
* You must set ec2_region variable to the region you wish to use (e.g. eu-west-1)
* You must set certificate_domain to the domain you wish to issue a certificate for (e.g. www.yoursite.com)

## How it works

Procedure is thus:

1. Try to get the ISSUED certificate, if one exists
2. Try to get the PENDING_VALIDATION certificate, if one exists
3. Request a new certificate if we don't have one at all
4. Wait for certificate DNS record to be made available
5. Create Route53 DNS record for the certificate
6. Wait for certificate to be validated

## Outputs

The playbook will set and log the certificate_arn fact. This is the ARN of the certificate that was found or generated
