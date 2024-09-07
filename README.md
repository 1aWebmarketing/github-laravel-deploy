# Deploy a laravel app through github to a managed server using github actions

## Prerequisites

We assume, that you already manage your laravel app in a github repository. When you just start with github we recommend using the GitHub Desktop client and the folling <code>.gitignore</code> List:

```
**/.DS_Store
/.phpunit.cache
/node_modules
/public/build
/public/hot
/public/storage
/storage/*.key
/vendor
.env
.env.example
.env.backup
.env.production
.phpactor.json
.phpunit.result.cache
Homestead.json
Homestead.yaml
auth.json
npm-debug.log
yarn-error.log
/.fleet
/.idea
/.vscode
```

## Prepare SSH Keys

As github builds your app and transfers it to your managed server via ssh, you will need a private SSH Key for your github and need to add the public key to your server-providers ssh account.

Add a new SSH Key Pair with the following command:

```
ssh-keygen -m PEM -t rsa -b 4096
```

Give it an absolute path with a name and 2 files should be generated. A **sshkeyname** file and **sshkeyname.public** file.

**Please Note:** You should not set a Passphrase (keep it empty)

## Setting up the variables

We will need a few github repository variables for this to work:
In your repository go to <code>Settings</code> <code>Secrets and variables</code> <code>Actions</code> and set the following variables and secrets:

| Type          | Name               | Value |
| ------------- |--------------------|-------|
| Variable      | SSH_HOST           | Hostname or IP of your server
| Variable      | SSH_USER           | SSH username
| Variable      | SSH_PATH           | Path to the folder, where your compiled laravel app should be copied /www/htdocs/w01f4....
| Secret        | SSH_PRIVATE_KEY    | Complete content of your private key file, usually starts with something like -----BEGIN RSA PRIVATE KEY-----

## Adding workflow to github

You can use the online repository viewer to add the workflow or add it by committing the workflow file <code>.github/workflows/nameyourworkflow.yml</code>

## Thats it

Check, if your workflow.yml is visible in your repository after committing. It should also be visible in the <code>Actions</code> Tab of your repository.
