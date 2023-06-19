# Migration between environments
Migration of structure and data in Strapi can be done in 3 ways, each with pros and cons.

## Import/Export plugin
The plugin allows for the export and import of structure and data between environments. 

> Note that the import/export plugin does not seem to import/export content files like images and documents. You will have to manually move those between environments (copy/paste)

The plugin can be found in the Strapi administration interface.
![image.png](/.attachments/image-c9bbaf08-2f47-48a9-9ce4-4226b7dfe1f0.png)

To export, click the `Export` button and select the appropriate settings.
![image.png](/.attachments/image-72b91d54-27d9-45df-8d09-f7d9956956f1.png)

To import, click the `Import` button and add the import file.
![image.png](/.attachments/image-a91cb689-197b-401e-82cf-28ace388ce49.png)

##Export, Import, and Transfer
Strapi CLI support functionality to move Strapi structure, data and content. See the [Strapi Data Management documentation](https://docs.strapi.io/dev-docs/data-management) for more information and usage.

> Note that `transfer` does not seem to be supported in Strapi versions 4.6 and lower. You will have to export, copy the file to the destination and import.

> Note that these migration methods replace all existing structure, data and content.

To export, open a command line (on Azure you can run this on the SSH virtual terminal for an App Service), change the directory to the root or the CMS web app and run the command:
`node node_modules/@strapi/strapi/bin/strapi.js export -f <FILE_NAME>`

![image.png](/.attachments/image-d355f1bb-2122-4b8b-bd02-5a240f258caa.png)

To import, open a command line (on Azure you can run this on the SSH virtual terminal for an App Service), change the directory to the root of the CMS web app and run the command: 
`node node_modules/@strapi/strapi/bin/strapi.js import -f <FILE_NAME>`

## Database backup and restore
You can create a backup of a Strapi database and restore it to a different environment.

> Note that a database backup and restore do not move content files like images and documents. You will have to manually move those between environments (copy/paste)

See [Export from UAT](https://dev.azure.com/NewMediaLabs/nml.co.za/_wiki/wikis/nml.co.za.wiki/3472/Strapi-CMS?_a=edit&anchor=export-from-uat) below for more information.

# Running Strapi locally for development
## Prequisites
- Source code for `cms.nml.co.za` repository
- Docker Desktop
  - Image for MySql `docker pull mysql`
  - Image for PhpMyAdmin `docker pull phpmyadmin`
- Azure Storage Emulator
  - Azurite
  - Azure Storage Explorer

# MySQL and PhpMyAdmin
## Environment variables
In order to start the containers via `docker compose` you need to create an environment variables file called `.docker-compose.env` in the root of the repository. 
> Do not add `.docker-compose.env` to the Git repository, because each developer should have their own version of it. It has been added to `.gitignore`

Add an environment variable line for `MYSQL_ROOT_PASSWORD`:
```
MYSQL_ROOT_PASSWORD=This-Should-Be-Your-Own-Password
```

## Docker Compose
In a terminal window, browse to the root folder for the repository and run
```
docker compose up
```

The terminal output will show whether either of the containers failed, but to test it you can browse to `http://localhost:8081`, and login into the PhpMyAdmin web application using `root` and the password specified in `.docker-compose.env`.

# Import the latest Strapi configuration
## Export from UAT
To replicate what exists in UAT, you can import the Strapi database from UAT. To do that you must log into the UAT MySQL from the PhpMyAdmin web application at `http://localhost:8082`. The password for `mysql-nmlcoza-cms-uat-sano.mysql.database.azure.com` can be found in the `kv-nmlcoza-uat-sano` Key Vault. 

> You will need to have access rights to it and be on the NML VPN.

![image.png](/.attachments/image-c7d26681-6f48-4dd2-952e-ff9d57687217.png)

Select the `nmlcozacmsuat` database, and click on `Export`

![image.png](/.attachments/image-54f9dd2e-9886-49f4-a919-86c2e49994eb.png)

## Import to local
To import the generated file, login into PhpMyAdmin at `http://localhost:8081`. Create a new database and call it `nmlcozacms`.
![image.png](/.attachments/image-f1ae5124-635a-47ad-bad2-4ee020b53ff7.png)
![image.png](/.attachments/image-03732c8b-e026-40de-a7fd-b78ff312da97.png)

Select the `nmlcozacms` database on the schemas list on the left, and click `Import` at the top.

![image.png](/.attachments/image-0b27a22a-46ec-4bff-a73e-aeaafab99f0a.png)

Choose the generated file and click `Import`. You will receive a success message once done.
![image.png](/.attachments/image-23aa1f7a-b168-42b2-8562-8ac3b9a2b875.png)

# Azure Storage
Strapi is configured to store media in an Azure Storage Account. Azurite is an Azure Storage emulator that allows local development without requiring Azure cloud instances.

## Azurite
Run `npm install -g azurite`

## Azure Storage Explorer
Download it from https://azure.microsoft.com/en-us/products/storage/storage-explorer/

# Configuring Strapi
You have to create a `.env` file that contains all the required environment variables.
> Do not add `.env` to the Git repository, because each developer should have their own version of it. It has been added to `.gitignore`

## Example `.env` file
```
## Server Settings
HOST=0.0.0.0
PORT=1337
APP_KEYS=8dcahebn5mv5QJ9yph8Fjhh7XLFfD6LRm9kKzQ8gmS9j8mCvhm5oyRHXYecdKm3k

## Admin Settings
API_TOKEN_SALT=9330263905638372362899741297207425673667696883050127399996218280
ADMIN_JWT_SECRET=8736888659206575320574611605661536169786317448846709052475511494

## Users-Permissions Plugin Settings
JWT_SECRET=eKMGOvS9QTwiWSqMWLh03Q==

## Database Settings
MYSQL_SERVER=localhost
MYSQL_DATABASE=nmlcozacms
MYSQL_USER_NAME=root
MYSQL_PASSWORD=This-Should-Be-Your-Own-Password

##Storage settings
STORAGE_ACCOUNT=devstoreaccount1
STORAGE_ACCOUNT_KEY=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
STORAGE_URL=http://127.0.0.1:10000/devstoreaccount1
STORAGE_HOST=127.0.0.1:10000
STORAGE_CONTAINER_NAME=ct-nmlcoza-cms


## General
STRAPI_LOG_LEVEL=trace
```
You should generate your own `APP_KEYS`, `API_TOKEN` and `ADMIN_JWT_SECRET` values, but it isn't required for development environments.

#Running Strapi
To run Strapi locally run `yarn develop` in a terminal at the root of your repository. Note that you will obviously have needed to run `yarn install` before to ensure the latest NPM packages are available.