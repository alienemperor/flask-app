Demo taken from https://realpython.com/flask-google-login/

#Flask-OIDC-APP

## How to run
### Requirements
- Docker
- Docker-Compose
- A running Keycloak environment (**must have SSL**)

### Build the container
1. Download the repository to your computer
1. In a terminal, navigate to the repository folder and run:
  - `docker build -t keycloak-flask:0.1 .`

### Set up the environment
1. Log in to your keycloak instance
1. Create a new realm (eg. Demo)
1. Open the new realm and create a new client
  1. Name the new client (eg. flask-app)
  1. Client Protocol: Openid-connect
  1. Set the Root URL to the URL the app will have (eg. https://localhost:5000)
    - **Note:** the app will run on https by default so do not use http:// in the URL
  1. Save
1. On the configuration page for the created client. Update *Access Type* to **confidential**, then save.
1. Move to the *Credentials* tab that should now be at the top of the client configuration page
1. Update the Docker-Compose.yml Environment variables with the Client ID and Secret (shown on the Credentials page)
1. navigate back to the *Realm Settings* page.
1. Right-click on the *OpenID Endpoint Configuration* link and copy link location
1. Update the docker-compose.yml DISCOVERY_URL environment variable with this link.
    - **Note:** this link should look like *https://<keycloakURL>/auth/realms/<RealmName>/.well-known/openid-configuration*
1. Save the docker-compose.yml file

### Run the App
1. In a terminal, navigate to the repository folder and run:
  - `docker-compose up -d`
1. Open a web browser and connect to https://localhost:5000
  - You will need to accept the self-signed certificate
1. Click the *Login* button and log in with a keycloak user. You will be presented with some of the user attributes and a *Logout* button.