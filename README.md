# HumanGov CI/CD Pipeline with AWS and Kubernetes



## HumanGov: Automating HumanGov SaaS Application Build and Deployment Process on Kubernetes with CI/CD Pipelines using AWS Code Commit, AWS Code Pipeline and AWS Code Build 

<p align="center">
<img src="https://i.imgur.com/TjcMPaN.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

## Project Description
The HumanGov application aims to streamline governance processes by providing a Software as a Service (SaaS) platform that facilitates citizen engagement and public service access. This project focuses on automating the software delivery process using Continuous Integration and Continuous Deployment (CI/CD) practices within AWS. The implementation leverages various AWS services to ensure efficient deployment, testing, and monitoring of the application across multiple environments, including development, staging, and production.

## Project Objectives
- **Automate Software Delivery**: Implement a CI/CD pipeline that enables automated deployment of code changes across multiple environments, reducing manual intervention and potential errors.
- **Enhance Code Quality**: Integrate automated testing in the pipeline to ensure only high-quality code is promoted to production.
- **Enable Staging for Validation**: Set up a staging environment that mirrors production to validate changes before they go live.
- **Facilitate Manual Approvals**: Introduce a manual approval step to enhance control over what gets deployed to production.

## Tools and Technologies
- **AWS CodeCommit**: For version control and source code management.
- **AWS CodePipeline**: For orchestrating the CI/CD workflow.
- **AWS CodeBuild**: For building Docker images and running tests.
- **Amazon Elastic Container Registry (ECR)**: For storing Docker images.
- **Amazon Elastic Kubernetes Service (EKS)**: For orchestrating containerized applications.
- **AWS Route 53**: For domain management and routing traffic to services.
- **AWS CloudFormation**: For infrastructure as code, managing AWS resources.

## Project Solution

### Part 1: CI/CD Pipeline Configuration
The initial setup involved creating a CodeCommit repository for the HumanGov application's source code. AWS CodePipeline was configured to automate the build and deployment process. The buildspec file was defined to include commands for building Docker images and running tests.

### Part 2: Testing Process
The testing phase was integrated into the pipeline, ensuring that automated tests were executed after each code change. If tests failed, deployment to production was halted, allowing developers to address issues before proceeding. A manual approval step was added, requiring explicit approval before production deployment.

### Part 3: Staging Environment Implementation
A staging environment was established to validate changes in a production-like setting. Modifications to deployment files were made to ensure the correct image versions were used for staging. After successful testing, a manual approval was required to promote changes to the production environment.

## Step-by-Step Directions

### Project Implementation: HumanGov Application CI/CD Pipeline Setup

### Step 1: Prerequisites Check and Setup:
**Access AWS Console and Cloud9:**
- Ensure access to the AWS Management Console and Cloud9 development environment.

**Verify Kubernetes Cluster:**
- Use kubectl get nodes to confirm authentication to the Kubernetes cluster.

<p align="center">
<img src="https://i.imgur.com/0xKxz6l.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/Md9dDhH.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### Step 2: Code Commit Repository Check:
**Confirm the presence of the Code Commit repository:**
- Access the AWS CodeCommit console.
- Verify the existence of the repository named human-gov-application containing the HumanGov application source code.

<p align="center">
<img src="https://i.imgur.com/RkLOfQK.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### Step 4: Committing Source Code Changes:
1. Navigate to the HumanGov application source code directory:

<p align="center">
<img src="https://i.imgur.com/kP1lUxn.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. Check the status of changes:

<p align="center">
<img src="https://i.imgur.com/Dh8z2ns.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

3. Add all changed files to the staging area:

<p align="center">
<img src="https://i.imgur.com/fxq0fKT.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

4. Commit the changes:

<p align="center">
<img src="https://i.imgur.com/S8wWtSW.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

5. Push the commit to the Code Commit repository:

<p align="center">
<img src="https://i.imgur.com/ziWXpAM.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### Step 5: AWS CodePipeline Configuration:
1. Access the AWS CodePipeline console.

2. Start creating a new pipeline named human-gov-cicd-pipeline.

<p align="center">
<img src="https://i.imgur.com/QIYGIkG.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

3. Configure the pipeline:
- Source Provider: AWS CodeCommit
- Repository: human-gov-application

<p align="center">
<img src="https://i.imgur.com/gFPfVSD.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Branch: master

<p align="center">
<img src="https://i.imgur.com/YZeM8O0.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Change Detection Options: AWS CloudWatch Events

<p align="center">
<img src="https://i.imgur.com/OrxcdGC.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Output Artifact Format: CodePipeline default

<p align="center">
<img src="https://i.imgur.com/UfzroTw.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

4. Add a build provider:
- Provider: AWS CodeBuild

<p align="center">
<img src="https://i.imgur.com/hnPdvSD.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Project: Create a new project named HumanGovBuild.

<p align="center">
<img src="https://i.imgur.com/n7sNPcH.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

5. Configure the CodeBuild project:
- Name: human-gov-build
- Region: US East 1
- Environment:
  - Managed image

<p align="center">
<img src="https://i.imgur.com/6fmORXa.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Amazon Linux 2 x86_64 standard 4.0

<p align="center">
<img src="https://i.imgur.com/UjYpm1g.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Privileged mode enabled

<p align="center">
<img src="https://i.imgur.com/gb5q5qK.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Additional Configuration: Select the EKS VPC and private subnets.

<p align="center">
<img src="https://i.imgur.com/FPnlgxo.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### Build Spec File Configuration:
1. Edit the build spec file to include necessary commands for the build process.
2. Ensure the AWS CLI is installed.
3. Set environment variables for the ECR repository URI.
4. Authenticate with ECR using AWS CLI.
5. Build the Docker image and tag it with appropriate versions.
6. Push the Docker image to ECR.
7. Export image tag to an environment variable and write it to an image definition file.

<p align="center">
<img src="https://i.imgur.com/D8SNQ4x.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

**Push the Docker image to ECR:**
- After building the Docker image, push it to the specified ECR repository.

<p align="center">
<img src="https://i.imgur.com/DAbr44x.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

**Export image tag to an environment variable and write it to an image definition file:**
- Export the image tag generated during the build process to an environment variable.

<p align="center">
<img src="https://i.imgur.com/tSSqsEQ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Write this image tag along with other necessary information to an image definition file (imagedefinitions.json). This file will be used during the deployment stage to specify the Docker image's location. Create Pipeline

<p align="center">
<img src="https://i.imgur.com/aydrJX4.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

**Add AmazonElasticContainerRegistryPublicFullAccess Permission to ECR on Service Role:**
- Navigate to the IAM console > Roles
- Search for the role created HumanGovBuild for Code Build

<p align="center">
<img src="https://i.imgur.com/Q4MrpTV.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Add the permission **AmazonElasticContainerRegistryPublicFullAccess** to it

<p align="center">
<img src="https://i.imgur.com/91pfGbZ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### Set Up AWS CodeBuild for Deploying the Application
**Create a Deployment Project:**
- Name the project differently (e.g., HumanGovDeployToProduction).

<p align="center">
<img src="https://i.imgur.com/aLglyQ4.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Set the environment variables AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY to the eks-user user credentials on Cloud Build.

<p align="center">
<img src="https://i.imgur.com/b1hSuoi.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Replace the Image URI placeholders in the humangov-california.yaml and humangov-florida.yaml files with CONTAINER_IMAGE.

<p align="center">
<img src="https://i.imgur.com/kLkTIDn.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

**Commit and push the changes:**

<p align="center">
<img src="https://i.imgur.com/6JfOP8M.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

**Testing the CI/CD Pipeline:**

<p align="center">
<img src="https://i.imgur.com/7yscSCL.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

## Part 2: Adding the Test Stage to HumanGov CI/CD Pipeline

1. **Add Source Code for Testing Simulation:**
- Create a new folder named tests under the human-gov-application/src directory.
- Inside the tests folder, create two files: app.py and test_app.py.

<p align="center">
<img src="https://i.imgur.com/fWMi7Lo.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. **Add Test Stage to the CI/CD Pipeline:**
- In the humangov-cicd-pipeline, add a new stage and action called HumanGovTest immediately after the HumanGovBuild stage.

<p align="center">
<img src="https://i.imgur.com/VH65ZHy.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Utilize the provided buildspec.yml for the test specification, ensuring to update the line with your ECR authentication line.

<p align="center">
<img src="https://i.imgur.com/sWquW1d.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Grant the AmazonElasticContainerRegistryPublicFullAccess permission to ECR on the service role codebuild-HumanGovTest-service-role.

<p align="center">
<img src="https://i.imgur.com/IXphlod.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Commit and push the changes to trigger the pipeline and observe the HumanGovTest stage running after the HumanGovBuild stage.

<p align="center">
<img src="https://i.imgur.com/3KugbLr.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/5iVmFk9.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

3. **Change the Test Scripts to Simulate Failure:**
- Modify the app.py file in the tests folder to introduce a deliberate mistake (e.g., removing the 'H' from 'Human' in the return string).

<p align="center">
<img src="https://i.imgur.com/pKsU1GW.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Commit and push the changes to simulate a developer mistake leading to a software bug.

<p align="center">
<img src="https://i.imgur.com/vAeaPta.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Observe the test failure, preventing deployment to the Kubernetes deployment.

<p align="center">
<img src="https://i.imgur.com/gtuwU0i.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/g6yrKtP.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

4. **Correct the Mistake and Verify:**
- Revert the changes made in the app.py file to fix the introduced mistake.

<p align="center">
<img src="https://i.imgur.com/O4PG1JS.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Commit and push the corrections.

<p align="center">
<img src="https://i.imgur.com/nUVVWiS.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Observe the successful execution of tests and deployment to the Kubernetes deployment.

<p align="center">
<img src="https://i.imgur.com/3Axxq5p.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/ZPmP4Pp.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

## Part 3: Simulating Continuous Delivery with Manual Approval

1. **Adding a Staging Environment:**
- Provision DynamoDB and an S3 bucket for the staging application using Terraform.

<p align="center">
<img src="https://i.imgur.com/fTypZL0.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Duplicate the Kubernetes deployment file and modify it for the staging environment.

<p align="center">
<img src="https://i.imgur.com/PEc5gCk.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Update the Ingress configuration to include the staging environment.

<p align="center">
<img src="https://i.imgur.com/4g4cNiA.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/oCFOK3g.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/O3gphnd.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Test the staging application (staging.cloudspecialist.click).

<p align="center">
<img src="https://i.imgur.com/PCs1yb1.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/3KX6IG8.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

2. **Incorporating Staging into CI/CD Pipeline:**
- Create a new CodeBuild project named HumanGovDeployToStaging to deploy changes to the staging environment.

<p align="center">
<img src="https://i.imgur.com/d97diE0.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Set environment variables for authentication with the EKS cluster.

<p align="center">
<img src="https://i.imgur.com/baDAc3g.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Define a custom buildspec.yml to deploy changes to the staging environment.

<p align="center">
<img src="https://i.imgur.com/LUVpnND.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Add a Manual Approval step after deploying to staging to transition from Continuous Deployment to Continuous Delivery.

<p align="center">
<img src="https://i.imgur.com/OeXKrCz.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Update the deployment file to replace the Image URI with a placeholder.

<p align="center">
<img src="https://i.imgur.com/wrXSedO.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

3. **Testing the CI/CD Pipeline:**
- Make a code change and commit it to trigger the CI/CD pipeline.
- Fix the BuildSpec of the HumanGovBuild project to include the staging deployment file.

<p align="center">
<img src="https://i.imgur.com/Nc4CnVt.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Re-run the pipeline and ensure successful deployment to staging.

<p align="center">
<img src="https://i.imgur.com/LXRw8GI.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Approve the manual approval step to deploy changes to the production environment.

<p align="center">
<img src="https://i.imgur.com/TKw9uET.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

## Project Conclusion
The implementation of the CI/CD pipeline for the HumanGov application significantly improved the software delivery process. Automated testing and the introduction of a staging environment enhanced code quality and reduced the risk of deploying faulty code. The manual approval process added an additional layer of control, ensuring that only validated changes reached production.

### Challenges Encountered
- **Configuration Errors**: Initial deployment failures were encountered due to missing files in the build spec. Troubleshooting was required to identify and rectify the issue.
- **Complexity of Pipeline Management**: As the pipeline grew more complex, managing various stages and ensuring proper resource allocation became challenging.

### Lessons Learned
- **Thorough Testing**: The importance of comprehensive testing in the CI/CD pipeline became evident, as early detection of issues saves time and resources.
- **Effective Troubleshooting**: Developing troubleshooting skills is crucial for quickly resolving issues that arise during the deployment process.

### Future Improvements
- **Enhanced Monitoring**: Implementing better monitoring tools to track pipeline performance and deployment success rates could provide deeper insights.
- **Automated Rollbacks**: Introducing automated rollback capabilities in the event of failed deployments could improve system reliability.
- **User Feedback Integration**: Establishing a feedback loop from users post-deployment to gather insights for continuous improvement of the application.
