### Hi there 👋

# Hey there! I'm Andrew 👋
<!-- <img src="wave.gif" width="26px"> -->

📫 How to reach me:
<p align="left">
    <a href="https://twitter.com/webstean"><img src="https://img.shields.io/badge/-Twitter-2D2B55?style=flat-square&logo=twitter&logoColor=white"/></a>
    <a href="https://www.linkedin.com/in/maketechwork/"><img src="https://img.shields.io/badge/-LinkedIn-2D2B55?style=flat-square&logo=linkedin&logoColor=white"/></a>
</p>

⚡ I am a technology architect, engineer, mentor, and cloud advocate with over 20 years professional experience. I specialise in designing the hosting of enterprise applications and solutions, principally in the Azure Cloud. I love a challenge and I'm skilled at progressing from a simple proposal into a well-defined, robust and production ready solution. My experence goes beyond the typical compute, network and storage, as I have been involved in several large consolidation and migration projects of Oracle and Microsoft SQL Server databases, sometimes involving virtualisation other times in (or out) of public clouds like AWS or Azure. 

🌱 I enjoy with working with developers and security/cyber indivduals, to help optimise their way of working and deliver better overall outcomes ensuring both security, reliability and agility to evolve as things change.

👯 I live and work in Melbourne, Australia. Over my career I have lived and worked in Singapore, Japan (Tokyo) and USA (North Carolina).

[Terraform](https://developer.hashicorp.com/terraform/docs) has been my new favourite bit of tech in the last few years - solves so many "infra" challenges in a simple, elegant and intuitive way.

Currentyl, I am enjoying full Terraform support in [AZD](https://github.com/Azure/azure-dev) and [ADE](https://learn.microsoft.com/en-us/azure/deployment-environments/how-to-configure-extensibility-model-custom-image), that can be used together to combined infrastructure provisioning and application deployment in the same step, including during GitHub Actions / ADO Pipelines -an example:- <br>
```shell
## Provision Infrastructure
azd provision
## Deploy Application
azd deploy
### or do both, with one step
azd up
```

## GitHub Stats

<a href="https://github.com/webstean">
  <img height="180em" src="https://github-readme-stats.vercel.app/api?username=webstean&show_icons=true&theme=shades-of-purple&count_private=true" alt="webstean's GitHub Stats" />
  <img height="180em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=webstean&theme=shades-of-purple&layout=compact" 
    alt="Andrew Webster GitHub Top Languages" />
</a>

<!--
**webstean/webstean** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->

# Some links to icons, pretty pictures etc... 💬

## Azure Links
Developer Portal       : https://devportal.microsoft.com<br> 
DevBox Portal          : https://devbox.microsoft.com/<br> 
Azure Portal           : https://portal.azure.com<br>
*Preview* Azure Portal : http://preview.portal.azure.com/<br>
*RC* Azure Portal      : http://rc.portal.azure.com/<br>
APIM CheatSheet        : https://github.com/Azure/api-management-policy-snippets/blob/master/policy-expressions%2FREADME.md/<br>

## Microsoft / Azure Icons
Azure             : https://learn.microsoft.com/en-us/azure/architecture/icons/<br>
Power Platform    : https://learn.microsoft.com/en-us/power-platform/guidance/icons<br>
Dynamics 365      : https://learn.microsoft.com/en-us/dynamics365/get-started/icons<br>
Microsoft 365     : https://learn.microsoft.com/en-us/microsoft-365/solutions/architecture-icons-templates?view=o365-worldwide<br>

## Terraform 
Terraform Awesome   : https://github.com/shuaibiyy/awesome-tf/blob/master/README.md<br>
Provider: Azurerm   : https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs<br>
Provider: Entra     : https://registry.terraform.io/providers/hashicorp/azuread/latest/docs<br>
Provider: AZAPI     : https://registry.terraform.io/providers/hashicorp/azuread/latest/docs<br>
Provider: PPlatform : https://registry.terraform.io/providers/microsoft/power-platform/latest/docs<br>
Provider: Fabric    : https://registry.terraform.io/providers/microsoft/fabric/latest<br>


## **Highly Recommended** - OIDC Federation (Open ID Connect) for Terraform providers with your pipelines.
Please use OIDC Federation (OpenID Connect) for better security, that way you require no secrets or certificatres to expired or get compromised.<br>
[Setting up Terraform Azure provider to use OIDC Federation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/guides/service_principal_oidc)<br>
[Setting up Terraform Entra ID provider to use OIDC Federation](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/guides/service_principal_oidc)<br>
[Setting up Terraform Power Platform provider to use OIDC Federation](https://registry.terraform.io/providers/microsoft/power-platform/latest/docs#authenticating-to-power-platform-using-a-service-principal-with-oidc)<br>

```hcl
## Example: Add a Federation identity for GitHub to an Azure Application 
resource "azuread_application_federated_identity_credential" "example_federation" {
  for_each = github_repository.example

  display_name   = "fedcred-example-github"
  application_id = azuread_application.yourapp.id
  audiences      = ["api://AzureADTokenExchange"]
  issuer         = "https://token.actions.githubusercontent.com"
  description    = "Federated identity for ...."
  ## permission for just the main branch
  subject        = "repo:${each.value.full_name}:ref:refs/heads/main"
  ## permission for the GitHub environmnet
  subject        = "repo:${each.value.full_name}:environment:${var.environment_name}"
}

## Example: Add a Federation identity for GitHub to an Azure User Managed Identity (UMI)
## This works, even if you don't have the ability to created applications within Entra ID 
resource "azurerm_federated_identity_credential" "example_federation" {
  for_each = github_repository.example

  name                = "fedcred-example-github"
  resource_group_name = azurerm_resource_group.example.name
  audience            = ["api://AzureADTokenExchange"]
  parent_id           = azurerm_user_assigned_identity.example.id
  issuer              = "https://token.actions.githubusercontent.com"
  ## permission for just the main branch
  subject             = "repo:${each.value.full_name}:ref:refs/heads/main"
  ## permission for the GitHub environmnet
  subject             = "repo:${each.value.full_name}:environment:${var.environment_name}"
}
```


