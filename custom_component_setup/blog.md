# Short summary

Below are steps that should be done in order to get the Component environment running on M1 Mac. I will update this later on in case these instructions prove to be insufficient.

## Setup

    npm install @servicenow/cli@quebec -g

The command installs legacy version of the CLI. Old CLI is used due to errors encountered in the newest version. Hopefully the new CLI will be fixed soon.

    now-cli project --name PROJECT-NAME

Creates a project and a scope into the instance.

    npm install

Installs initial dependencies.

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

