# Publishing github wiki as Azure static webapp

Proof of concept on how to publish a github wiki to another Azure Static web apps. 
Usecase is privetly sharing wiki content with a finegrained audience of whom not all have a github account.
All users have an Azure Active Directory account and an azure subscription is available. 

## key-components

- publishing workflow [.github/workflows/azure-static-web-apps-from-wiki.yml](.github/workflows/azure-static-web-apps-from-wiki.yml)
   - triggerd by [gollum](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#gollum) trigger
   - checks out wiki to docs folder
   - installs [mkdocs](https://www.mkdocs.org/)
   - TODO: writes [mkdocs config](https://www.mkdocs.org/user-guide/configuration/) to `mkdocs.yml`
   - TODO: builds site using mkdocs
   - TODO: runs publish to static site
- TODO: infra deploy workflow [.github/workflows/deploy-azure-template.yml]


