# Initial Setup and Running App on Local Machine (Windows edition)

## Work Environment

There are two environments you will be working in for the exercises today.

1. **Local workstation:** The apps and containers must be run on a Linux machine. 

Install the following items:
Node JS - https://nodejs.org/en/download/
Azure CLI - https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest
MongoDB - https://www.mongodb.com/download-center#community
Docker CE - https://store.docker.com/editions/community/docker-ce-desktop-windows

2. **Azure Cloud Shell:** The Azure Cloud Shell will be accessed by logging into the Azure Portal (http://portal.azure.com).

Labs 1 and 2 will be completed on your local machine. The subsequent labs all use the Azure Cloud Shell.

## Clone Lab Github Repo

Once you have accessed the jumpbox, you must clone the workshop repo to the machine.

1. Start with a terminal on the jumpbox
2. Clone the Github repo via the command line

    ```
    git clone https://github.com/johnkeithwood/blackbelt-aks-hackfest.git
    ```

## Get Applications up and running

### Database layer - MongoDB

The underlying data store for the app is [MongoDB](https://www.mongodb.com/ "MongoDB Homepage"). It is already running. We need to import the data for our application.

1. Import the data using a terminal session on the jumpbox

    ```bash
    cd ~/blackbelt-aks-hackfest/app/db

    mongoimport --host localhost:27017 --db webratings --collection heroes --file ./heroes.json --jsonArray
    mongoimport --host localhost:27017 --db webratings --collection ratings --file ./ratings.json --jsonArray
    mongoimport --host localhost:27017 --db webratings --collection sites --file ./sites.json --jsonArray
    ```

### API Application layer - Node.js

The API for the app is written in javascript, running on [Node.js](https://nodejs.org/en/ "Node.js Homepage") and [Express](http://expressjs.com/ "Express Homepage")

1. Update dependencies and run app via node in a terminal session on the jumpbox

    ```bash
    cd ~/blackbelt-aks-hackfest/app/api

    npm install
    npm run localmachine
    ```

2. Open a new terminal session on the jumpbox and test the API

Browse to <http://localhost:3000/api/heroes>

### Web Application layer - Vue.js, Node.js

The web frontend for the app is written in [Vue.js](https://vuejs.org/Vue "Vue.js Homepage"), running on [Node.js](https://nodejs.org/en/ "Node.js Homepage") with [Webpack](https://webpack.js.org/ "Webpack Homepage")

1. Open a new terminal session on the jumpbox
2. Update dependencies and run app via node

    ```bash
    cd ~/blackbelt-aks-hackfest/app/web

    npm install
    npm run localmachine
    ```
3. Test the web front-end

    Browse to <http://localhost:8080>
    

## Clean-up

Close the web and api apps in the terminal windows by hitting `ctrl-c` in each of the corresponding terminal windows
