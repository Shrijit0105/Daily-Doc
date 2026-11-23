AWS Automated Deployment Pipeline — Project Log
Project: Automated Static Web App Pipeline on AWS
Status: 🟡 In Progress — Pipeline configured; automated deployment is not yet implemented
Project type: Beginner cloud / DevOps project
Date: 23 November 2026

1. Overview
This project is my first hands-on AWS project. The goal is to build an automated workflow that takes a web application packaged as a ZIP file, processes it through an AWS pipeline, and eventually deploys it to a hosting environment.

At the current stage, I have configured the source and build portions of the pipeline. The deployment stage and a verified automatic trigger are still pending.
2. Current Architecture
```mermaid
flowchart LR
    A[Web app files] --> B[ZIP archive: my-app.zip]
    B --> C[S3 source bucket: my-app-source-builds]
    C --> D[CodePipeline: my-app-pipeline]
    D --> E[Source stage]
    E --> F[Build stage: inline commands]
    F --> G[Build output / next deployment step]
```
3. AWS Resources Configured
Resource	Name	Purpose	Status
Amazon S3 bucket	my-app-source-builds	Stores the application ZIP file used as the pipeline source	Configured
AWS CodePipeline	my-app-pipeline	Orchestrates the pipeline stages	Configured
AWS CodeBuild project	my_app_build	Created for build-related tasks; currently not actively used by the pipeline because build commands are inline	Created


4. Pipeline Stages
Source Stage
- Uses an S3 bucket as the source provider.
- The source artifact is my-app.zip.
- The archive contains the static web application files (for example, index.html).
Build Stage
- Configured in CodePipeline.
- Uses inline build commands at the current stage of the project.
- A separate CodeBuild project (my_app_build) exists, but is not currently the active build action in this pipeline.
Deploy Stage — Pending
A deployment stage has not been configured yet. The eventual target may be an S3 static website or another hosting service, depending on the deployment design.
5. Intended Workflow
The intended end-to-end workflow is:
1. Update the static web app files.
2. Package the files into a ZIP archive.
3. Upload my-app.zip to the source S3 bucket.
4. Have the pipeline detect the source update and start automatically (trigger configuration/verification is still pending).
5. Run the configured build stage.
6. Deploy the resulting app to a hosting destination (not implemented yet).
6. What I Have Learned So Far
- The role of Amazon S3 as a storage and source-artifact location.
- How AWS CodePipeline organizes a CI/CD workflow into stages and actions.
- The difference between a pipeline's orchestration role and a build service/project.
- How build commands can be configured directly in a pipeline action.
- The distinction between continuous integration/build processing and continuous deployment: a pipeline that builds an artifact is not yet a complete deployment pipeline.
7. Current Progress
- [x] Created the source S3 bucket.
- [x] Prepared the application ZIP source artifact.
- [x] Created the CodePipeline pipeline.
- [x] Configured the Source stage.
- [x] Configured the Build stage with inline commands.
- [x] Created a separate CodeBuild project.
- [ ] Configure and verify automatic pipeline triggering on source updates.
- [ ] Add a deployment stage.
- [ ] Choose and configure the hosting target.
- [ ] Test the complete upload-to-deployment workflow.
- [ ] Document the final architecture and deployment result.
8. Next Steps
1. Finish configuring and test the source-change trigger.
2. Decide on a deployment target (for example, an S3 static website).
3. Add the Deploy stage to CodePipeline.
4. Configure permissions carefully using IAM least privilege.
5. Upload a new version of the application and verify the pipeline runs end-to-end.
6. Confirm that the deployed website reflects the updated source.
9. Project Reflection
This project is helping me understand AWS through practical implementation instead of treating cloud services as isolated concepts. So far, I have built the initial pipeline structure and connected the source and build stages. My next milestone is turning this pipeline into a working automated deployment workflow.
