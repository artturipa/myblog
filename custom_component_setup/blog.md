# Short summary

Below are steps that should be done in order to get the Component environment running on M1 Mac. I will update this later on in case these instructions prove to be insufficient.

## Setup (legacy CLI)

    npm install @servicenow/cli@quebec -g

The command installs legacy version of the CLI. Old CLI is used due to errors encountered in the newest version. Hopefully the new CLI will be fixed soon.

    now-cli project --name PROJECT-NAME

Creates a project and a scope into the instance.

    npm install

Installs initial dependencies.

## Setup (new CLI)

### Mac CLI installation

When I initially installed it, ServiceNow had not registered the application and the installer couldn't be opened.

It can be bypassed by running following command in installer's directory:

    $ xattr -d com.apple.quarantine NOW_INSTALLER_FILENAME

After installing the CLI, add UI Component extension:

    $ snc extension add --name ui-component

Connect to instance

    snc configure profile set

Create a project

    snc ui-component project --name @org/scope-name

Install dependencies

    npm install

Add dependencies

    npm install @servicenow/DEPENDENCY 
    npm install @servicenow/ui-effect-http

Develop

    snc ui-component develop

## M1 Mac environment setup

### Setup Rosetta-Terminal

Duplicate Terminal from applications

Right click new terminal / Get Info / Open using Rosetta = true

Rename as Rosetta Terminal

### Install Tools With Rosetta Terminal

Install NVM

    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash

Install Node

    nvm install 12

