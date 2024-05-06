# aquanar-backup

This repository holds the definitions needed to store backups from live and nonlive environments into a dedicated backup account.

# What does the backup repository contain?
Currently we are backing up the following resources:

* Terraform s3 state bucket
* AWS Secrets
* Mongodb backup, we are using mongo cloud backup strategy( until mvp golive)

# AWS Secrets Backup & Restore
AWS secrets are replicated to backup account (Europe (Ireland)eu-west-1) every day at 1am UTC using AWS lambda.

# Backup strategy
* Create one role per account nonlive, live and infra using account setup repo which can READ all the secrets in that account.
* Create 3 Lambdas in backup account which can assume the above corresponding role and create the secrets in backup account.
* use / naming strategy for the secrets in backup account.
* Create a cloudwatch rule to trigger the lambda once in a day.
* To assume role in another account check https://aws.amazon.com/premiumsupport/knowledge-center/lambda-function-assume-iam-role/
* Update the secret policy, so that backup lambda can read the secret value.

# [MongoDB restore strategy](https://github.com/otto-ec/aquanar_starter/blob/main/disaster-recovery/disaster-recovery.md#data-backup-to-drnonlive-aquanar-backup)
