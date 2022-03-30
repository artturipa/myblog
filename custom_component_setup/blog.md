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

## Deploy for multiple instances and companies

Add profiles for different instances

    snc configure profile set --profile PROFILE_NAME

Deploy component to specified instance:

    snc ui-component deploy --profile PROFILE_NAME

If the instance has different company prefix, component name should reflect that. Usually company specific prefix is five letters long symbol. So if you wan't to deploy the component to a company which has prefix of "xyzab", do following changes:

**In index.js:**

Look up for

    createCustomElement('xxxxx-component-name', {...

And change it to

    createCustomElement('xyzab-component-name', {...

**In now-ui.json:**

In the beginning of file there is section:

    {
        "components": {
        "xxxxx-component-name": { ...

Change it to:

    {
        "components": {
        "xyzab-component-name": { ...


## Fix "process is not defined" error in component development

1) Add "react-error-overlay": "6.0.9" into devDependencies in package.json

2) Run npm i --save-dev react-error-overlay@6.0.9 