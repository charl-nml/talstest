#Enviroments
There are two environments for the cms.nml.co.za project:
- UAT
- Production

## UAT
UAT deploys to the `app-nmlcoza-cms-uat-sano` Azure App Service.

## Production
Production deploys to the `app-nmlcoza-cms-prod-sano` Azure App Service.

# Builds
There are two builds:
- [CI-cms.nml.co.za](https://dev.azure.com/NewMediaLabs/nml.co.za/_build?definitionId=160)
- [CD-cms.nml.co.za-UAT](https://dev.azure.com/NewMediaLabs/nml.co.za/_build?definitionId=159)

The continuous integration (CI) build runs for PRs and changes to the `main` branch. 

The continuous deployment (CD) build runs automatically on merge changes to `main`.

# Releases
There is one release for the cms.nml.co.za project:
- [nmlcoza-CMS](https://dev.azure.com/NewMediaLabs/nml.co.za/_release?_a=releases&view=mine&definitionId=4)
  - Creates a release automatically and initiates a deployment immediately once the CD build completes.The release is deployed to UAT immediately. Production needs to be triggered manually for a release. 