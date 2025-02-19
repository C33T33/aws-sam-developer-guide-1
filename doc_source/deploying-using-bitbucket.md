# Deploying using Bitbucket Pipelines<a name="deploying-using-bitbucket"></a>

To configure your [Bitbucket Pipeline](https://support.atlassian.com/bitbucket-cloud/docs/get-started-with-bitbucket-pipelines/) to automate the build and deployment of your AWS SAM application, your `bitbucket-pipelines.yml` file must contain lines that do the following:

1. Reference a build container image with the necessary runtime from the available images\. The following example uses the `public.ecr.aws/sam/build-nodejs14.x` build container image\.

1. Configure the pipeline stages to run the necessary AWS SAM command line interface \(CLI\) commands\. The following example runs two AWS SAM CLI commands: sam build and sam deploy \(with necessary options\)\.

This example assumes that you have declared all functions and layers in your AWS SAM template file with `runtime: nodejs14.x`\.

```
image: public.ecr.aws/sam/build-nodejs14.x

pipelines:
  branches:
    main: # branch name
      - step:
          name: Build and Package
          script:
            - sam build
            - sam deploy --no-confirm-changeset --no-fail-on-empty-changeset
```

For a list of available Amazon Elastic Container Registry \(Amazon ECR\) build container images for different runtimes, see [Image repositories](serverless-image-repositories.md)\.