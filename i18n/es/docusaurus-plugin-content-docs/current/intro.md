---
sidebar_position: 1
---

# Introduction

**Bitbucket Pipelines** is a powerful cloud-based continuous integration (CI) and continuous delivery (CD) service fully integrated into Bitbucket. It allows you to automate software development workflows, from building and testing your code to deploying it to production. With Pipelines, you can define a series of steps that are automatically executed every time changes are made to your codebase, ensuring faster and more reliable releases.

In this guide, we will walk you through the basics of Bitbucket Pipelines and how to set up your first pipeline.

## Key Concepts

Before you begin setting things up, it's useful to understand some key concepts in Bitbucket Pipelines:

1. **Pipelines**: A pipeline is a set of automated processes that are triggered by events, such as pushing new code to your repository. These processes can include tasks like running tests, building the project, or deploying the application.

2. **bitbucket-pipelines.yml**: This is the configuration file where you define your pipeline. It’s a YAML file located at the root of your repository. This file tells Bitbucket Pipelines what steps to run and in what order.

3. **Steps**: Each step of a pipeline is a command or script that runs inside a Docker container. Steps can be executed sequentially or in parallel.

4. **Branches**: You can configure pipelines to run on specific branches, allowing for different workflows for development, testing, and production environments.

## Setting Up Your First Pipeline

To get started with Bitbucket Pipelines, follow these steps:

### Step 1: Enable Bitbucket Pipelines

1. Go to your repository in Bitbucket.
2. On the left sidebar, click on **Pipelines**.
3. Click the **Create your first pipeline** link. This will take you the starter pipeline where you can define your pipeline or use a template depending on your project.
4. Select the **Starter pipeline**

### Step 2: Configure the `bitbucket-pipelines.yml` File

The `bitbucket-pipelines.yml` file defines the steps of your pipeline. Here is a simple configuration example to get you started:

```yaml
image: node:14

pipelines:
  default:
    - step:
        name: Build and Test
        caches:
          - node
        script:
          - npm install
          - npm test
          - npm run build
        artifacts:
          - ./dist
