# Publishing github wiki as Azure static webapp

Proof of concept on how to publish a github wiki to another Azure Static web apps. 
Usecase is privetly sharing wiki content with a finegrained audience of whom not all have a github account.
All users have an Azure Active Directory account and an azure subscription is available. 

## key-components

- publishing workflow [.github/workflows/azure-static-web-apps-from-wiki.yml](.github/workflows/azure-static-web-apps-from-wiki.yml)
   - triggerd by [gollum](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#gollum) trigger
   - checks out wiki to docs folder
   - installs [mkdocs](https://www.mkdocs.org/)
   - writes [mkdocs config](https://www.mkdocs.org/user-guide/configuration/) to `mkdocs.yml`
   - formats filename as title and add to frontmatter to match github behaviour
   - renames home.md to index.md to make it the landing page under mkdocs
   - builds site using mkdocs
   - runs publish to static site
- TODO: infra deploy workflow [.github/workflows/deploy-azure-template.yml]

## deploy and configure

- login to azure and deploy infra
```
az login
az resourcegroup create \
   --resource-group <resourcegroupname>\
   --location <location>
az deployment group create \
   --resource-group <resourcegroupname> \
   --template-file ./infra/azuredeploy.json \
   --parameters ./infra/azuredeploy.parameters.json
```

- get deployment token from the azure portal.
- add token to github workflow secrets `AZURE_STATIC_WEB_APPS_API_TOKEN`
- update wiki and enjoy




