# Artifact Bucket Setup
Create a bucket to store deployment and build artifacts for a region

## Prerequisites
[AWS CLI](http://docs.aws.amazon.com/rekognition/latest/dg/setup-awscli.html)

## Dependencies
- [Logging Bucket CloudFormation Repo](https://github.com/benoram/oramco.aws.setup.loggingbucket.git)

## Setup
FailureToleranceCount is set to 1 since sa-east-1 does not have a logging bucket.

Run in the GitHub repo dir. This commands below use StackSets to deploy to all regions

```
aws cloudformation create-stack-set --stack-set-name ArtifactBuckets --template-body file://./cfn-artifact-bucket.yaml --region us-east-1

TEMP_ACCOUNTID='TheAccountId'
TEMP_ALLREGIONS=$(aws ec2 describe-regions --query 'Regions[].{Name:RegionName}' --output text | paste -sd " " -)
aws cloudformation create-stack-instances --stack-set-name ArtifactBuckets --accounts $TEMP_ACCOUNTID --regions $TEMP_ALLREGIONS --region us-east-1 --operation-preferences FailureToleranceCount=1