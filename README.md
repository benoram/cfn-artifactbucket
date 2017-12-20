# Artifact Bucket Setup
Create a bucket to store deployment and build artifacts for a region

## Prerequisites
[AWS CLI](http://docs.aws.amazon.com/rekognition/latest/dg/setup-awscli.html)

## Dependencies
- [Logging Bucket CloudFormation Repo](https://github.com/benoram/oramco.aws.setup.loggingbucket.git)

## Setup
Run in the GitHub repo dir and add a --region argument if you need to run in a region that isn't the default.

```
aws cloudformation create-stack --stack-name rArtifactBucket --template-body file://./cfn-artifact-bucket.yaml
```
