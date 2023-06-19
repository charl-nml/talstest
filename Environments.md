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