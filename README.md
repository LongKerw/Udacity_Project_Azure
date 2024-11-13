Resource Group
Resource Group Name: ssm
2. SQL Database
DB name: ssmdb
Server: ssmserver1.database.windows.net
DB region: us-central US
Admin login: cmsadmin
Admin password: CMS4dmin
Resource group: ssm
DB workload env: Development
DB compute + storage: DTU - Basic
Press the "Next: Networking" button, then select "Public Endpoint", and set both of the Firewall rules that appear to "Yes".
Set everything else to default
Run SQL queries in sql_scripts/ directory after completion, starting from the users table. Don't forget to take screenshots.
3. Storage Account
Resource group: ssm
Storage account name: ssmimages1 (needs to be unique)
Advanced - Allow enabling anonymous access on individual containers: Enable
Advanced - Access tier: Cool
Network access: Enable public access from all networks (the default)
Create container named "images". Set its access level to Container.
From Security + networking > Access keys:
Blob Storage key: ZUC7xqEJTizN3cWAruDl78GrkTIEbOb1pFjtHDUn2VGNcLyion9b9uWPDhclR1AqNhllnYD+68aF+ASttabtjw==

4. Microsoft Entra ID
4.1. App Registration
Name: ssmEntraID
Who can use? "Accounts in any organizational directory (Any Microsoft Entra ID tenant - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)"
4.2. Secret Creation
Secret description: cmsSecret
Secret Key: 2aef7b5a-eca4-4d3f-a29e-574c714d5646
Client Secret: jfo8Q~f-xxpeCwqpC2R8mve2IRwU_kxca0V-LaTe
Application (client) ID: 8b78175e-e4fb-4143-92e7-a66c5cdda205

Application
Name: udacitycms12.azurewebsites.net
Runtime stack: Python 3.10
Pricing Plan: Free F1
If you are getting a "Validation failed for a resource" error, pick a different region.
After creation:

Settings -> Environment variables - Add the following variables (sample values are included, replace them with your values):
BLOB_ACCOUNT: ssmimages1
BLOB_CONTAINER: images
BLOB_STORAGE_KEY: ZUC7xqEJTizN3cWAruDl78GrkTIEbOb1pFjtHDUn2VGNcLyion9b9uWPDhclR1AqNhllnYD+68aF+ASttabtjw==

SQL_SERVER: ssmserver1.database.windows.net
SQL_DATABASE: ssmdb
SQL_USER_NAME: cmsadmin
SQL_PASSWORD: CMS4dmin
CLIENT_SECRET: jfo8Q~f-xxpeCwqpC2R8mve2IRwU_kxca0V-LaTe
SECRET_KEY: 2aef7b5a-eca4-4d3f-a29e-574c714d5646
CLIENT_ID: 8b78175e-e4fb-4143-92e7-a66c5cdda205
Deployment Center
Source: GitHub
Pick the repo that contains the starter files.
6. Setting up OAuth2
At this point, your application should already be running. You should already be able to log in with username admin and password pass and you can create new posts or update existing ones.

The next part is getting the OAuth2 login to work.

Go to Microsoft Entra ID > App Registrations, click on the App Registration created earlier, and then pick Authentication from the left sidebar.

6.1. Microsoft Entra ID - Authentication - Add a Platform - Web
Redirect URIs: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/getAToken
logout URL: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/login
