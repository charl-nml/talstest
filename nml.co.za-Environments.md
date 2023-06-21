#Enviroments
There are two environments for the nml.co.za project:
- UAT
- Production

## UAT
UAT deploys to the `app-nmlcoza-uat-sano` Azure App Service.

## Production
Production deploys to the `app-nmlcoza-prod-sano` Azure App Service.

# Builds
There are three builds:
- [CI-nml.co.za](https://dev.azure.com/NewMediaLabs/nml.co.za/_build?definitionId=177)
- [CD-nml.co.za-UAT](https://dev.azure.com/NewMediaLabs/nml.co.za/_build?definitionId=178)
- [CD-nml.co.za-PROD](https://dev.azure.com/NewMediaLabs/nml.co.za/_build?definitionId=179)

The continuous integration (CI) build runs for PRs and changes to the `main` branch. It is configured with Sonar Cloud for code quality checks.

The continuous deployment (CD) builds are configured to run using the equivalent environment CMS by default, but this can be explicitly specified for testing and sign-off reasons. 

The UAT CD build runs automatically on merge changes to `main`. The production CD build runs on-demand only.

The setup is configured this way to allow the development team to test and sign off both production content-only changes and CMS structure changes in UAT, before going live.

## Creating a UAT build for production content-only changes
1. Update production CMS with content changes
1. Click `Run Pipeline` for [CD-nml.co.za-UAT](https://dev.azure.com/NewMediaLabs/nml.co.za/_build?definitionId=178)
1. Click `Variables`
![image.png](/.attachments/image-134802f1-167e-49c4-a584-f2343b5815c9.png)
1. Modify the variable with the appropriate values for the Production CMS
![image.png](/.attachments/image-a860f8af-f424-4e8f-96d2-105a8bd5694a.png)
1. Click `Run`

This will initiate a build against the production CMS data and release it to the UAT App Service.

# Releases
There are two releases for the nml.co.za project:
- [nml.co.za UAT](https://dev.azure.com/NewMediaLabs/nml.co.za/_release?_a=releases&view=mine&definitionId=6)
  - Creates a release automatically and initiates a deployment immediately once the CD build completes.
- [nml.co.za Production](https://dev.azure.com/NewMediaLabs/nml.co.za/_release?_a=releases&view=mine&definitionId=7)
  - Creates a release automatically once the CD build completes. A deployment needs to be triggered manually. 