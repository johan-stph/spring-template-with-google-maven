# Deploy a (Spring) Application to Google Cloud with a Database

This guide will walk you through deploying a Spring application to Google Cloud Platform (GCP) with a database.

### What you'll need

1. Create a Google Account at https://console.cloud.google.com/
2. Create a new project - organisation name is optional and not really important. The name of the project is also not important, because it is later referred to by the project ID, which is a unique identifier.
3. After the project is created, you will be redirected to the project dashboard. If not select the project from the top left dropdown menu.
4. Now visit the [Cloud SQL](https://console.cloud.google.com/sql) page and click on the "Create Instance" button.
5. In this project a PostgreSQL database will be used but feel free to use any other database that is supported by Cloud SQL.
6. If the Compute Engine API is not enabled, you will be prompted to enable it. Click on the "Enable" button.
7. Name the database instance and set a password for the postgres user. You need to remember this password, because it will not be stored in gcp.
8. Now select the region and zone where the database will be deployed. The region and zone should be the same as the region and zone where the application will be deployed. For optimal performance, the region and zone should be the same as the region and zone where the user is located. https://gcping.com/
9. For this demo example make sure to select in each menu the cheapest option. Scaling the database up or down is possible at any time.
10. Make sure you give the database a public IP address. To manage the database from outside GCP.
11. (Optional) It is possible to create your own database, the default one is "postgres" and is created automatically. https://cloud.google.com/sql/docs/postgres/create-manage-databases
12. Install the Google cloud sdk https://cloud.google.com/sdk/docs/install
13. Follow the instructions to authenticate the sdk with your Google account.
14. (Optional) You have the option to install the cloud sql proxy. This is not necessary, but it will make it easier to connect to the database from outside GCP or with database management tools. https://cloud.google.com/sql/docs/postgres/connect-auth-proxy
    1. ```curl -o cloud-sql-proxy https://storage.googleapis.com/cloud-sql-connectors/cloud-sql-proxy/v2.1.2/cloud-sql-proxy.linux.amd64```
    2. ```chmod +x cloud-sql-proxy```
    3. ```./cloud_sql_proxy -instances={TODO: Insert Instance Name}=tcp:0.0.0.0:5432```
    4. Now you can connect to the database locally on port 5432. http://localhost:5432


### Spring Setup
1. Use this repository as a template and create a new repository.
2. The required dependencies are already included in the pom.xml file. If you want to use a different database, you need to change the dependencies in the pom.xml file.
3. The application.yaml file contains the configuration for the profile. Then the corresponding application-{profile}.yaml file is loaded. The active profile can and should be overwritten by an environment variable for local testing and development.

### Google Cloud Workflow Setup
1. Copy and follow the instructions google-cloud-deployment workflow in the .github/workflows folder.