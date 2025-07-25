### Hey there! I'm Andrew <img src="https://blog.joypixels.com/content/images/2019/06/waving_hand_sign_1024.gif" width="40px">
<br>
<a href="https://twitter.com/webstean" target="_blank">
  <img src="https://img.shields.io/badge/Twitter-@webstean-1DA1F2?style=flat&logo=twitter&logoColor=white" alt="Twitter Badge"/>
</a>
<a href="https://www.linkedin.com/in/maketechwork/" target="_blank">
  <img src="https://img.shields.io/badge/LinkedIn-MakeTechWork-0077B5?style=flat&logo=linkedin&logoColor=white" alt="LinkedIn Badge"/>
</a>
<a href="mailto:webstean@gmail.com">
  <img src="https://img.shields.io/badge/Email-webstean@gmail.com-D14836?style=flat&logo=gmail&logoColor=white" alt="Email Badge"/>
</a>
<br>

## 📄 About Me
<br>
⚡ I am a IT architect, engineer, mentor, and cloud advocate with over 20 years professional experience. I specialise in designing the hosting of enterprise applications and solutions, principally in the Azure Cloud. I love a challenge and I'm skilled at progressing from a simple proposal into a well-defined, robust and production ready solution. My experence goes beyond the typical compute, network and storage, as I have been involved in several large consolidation and migration projects of Oracle and Microsoft SQL Server databases, sometimes involving virtualisation other times in (or out) of public clouds like AWS or Azure.<br> 

🌱 I enjoy with working with developers and security/cyber indivduals, to help optimise their way of working and deliver better overall outcomes ensuring both security, reliability and agility to evolve as things change.<br>

👯 I live and work in [Melbourne, Australia](https://en.wikipedia.org/wiki/Melbourne). But over my career I have lived and worked in [Singapore](https://en.wikipedia.org/wiki/Singapore), [Tokyo, Japan](https://en.wikipedia.org/wiki/Tokyo) and [North Carolina, USA](https://en.wikipedia.org/wiki/North_Carolina).<br>

[Terraform](https://developer.hashicorp.com/terraform/docs) has been my new favourite bit of tech in the last few years - solves so many "infra" challenges in a simple, elegant and intuitive way.<br> I just love how I can deploy totally repeatable infrastructure accorss multiple cloud regions. I've even used to managed VMware ESXi clusters.

Currently, I am enjoying the full Terraform support in [AZD](https://github.com/Azure/azure-dev) and [ADE](https://learn.microsoft.com/en-us/azure/deployment-environments/how-to-configure-extensibility-model-custom-image), that can be used together to combined infrastructure provisioning and application deployment in the same step. This is particularly useful during GitHub Actions / ADO Pipelines -as an example:- <br>
```shell
## Provision Infrastructure
azd provision
## Deploy Application
azd deploy
### or do both, with one step
azd up
```
See [here](https://learn.microsoft.com/en-us/azure/developer/azure-developer-cli/) and [here](https://learn.microsoft.com/en-us/azure/deployment-environments/) for the complete documentation

## 📄 Some GitHub States
<br>
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
<br>
<br>

## 📄 Some Useful Links

#### Azure Portal Links
Developer Portal       : https://devportal.microsoft.com<br> 
DevBox Portal          : https://devbox.microsoft.com/<br> 
Azure Portal           : https://portal.azure.com<br>
*Preview* Azure Portal : http://preview.portal.azure.com/<br>
*RC* Azure Portal      : http://rc.portal.azure.com/<br>
APIM CheatSheet        : https://github.com/Azure/api-management-policy-snippets/blob/master/policy-expressions%2FREADME.md/<br>

#### Microsoft / Azure Icons
Azure             : https://learn.microsoft.com/en-us/azure/architecture/icons/<br>
Power Platform    : https://learn.microsoft.com/en-us/power-platform/guidance/icons<br>
Dynamics 365      : https://learn.microsoft.com/en-us/dynamics365/get-started/icons<br>
Microsoft 365     : https://learn.microsoft.com/en-us/microsoft-365/solutions/architecture-icons-templates?view=o365-worldwide<br>

#### Terraform 
Terraform Awesome        : https://github.com/shuaibiyy/awesome-tf/blob/master/README.md<br>
Provider: Azurerm        : https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs<br>
Provider: Entra          : https://registry.terraform.io/providers/hashicorp/azuread/latest/docs<br>
Provider: azapi          : https://registry.terraform.io/providers/hashicorp/azuread/latest/docs<br>
Provider: Power Platform : https://registry.terraform.io/providers/microsoft/power-platform/latest/docs<br>
Provider: Fabric         : https://registry.terraform.io/providers/microsoft/fabric/latest<br>
Azure Verified Modules   : https://azure.github.io/Azure-Verified-Modules/<br>

## 📄 **My Top Tip** - Use OIDC Federation (Open ID Connect)
When using Terraform providers as part of GitHub / Dev Ops actions / pipelines, please use OIDC Federation (OpenID Connect) for better security, that way you require no secrets or certificatres to expired or get compromised.<br>
This works and fully support with both GiutHub Actions and Azure DevOps (ADO) pipelines. The relevant documentation links can be found below:<br>
[Setting up Terraform Azure provider to use OIDC Federation](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/guides/service_principal_oidc)<br>
[Setting up Terraform Entra ID provider to use OIDC Federation](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/guides/service_principal_oidc)<br>
[Setting up Terraform Power Platform provider to use OIDC Federation](https://registry.terraform.io/providers/microsoft/power-platform/latest/docs#authenticating-to-power-platform-using-a-service-principal-with-oidc)<br>

```hcl
## Example: Add a Federation identity for GitHub to an Azure Application
## Generally, I'd recommend using the alterantive (User Assigned Identity) as per below
## as its a smaller footprint
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
  subject        = "repo:${each.value.full_name}:environment:${var.environment_name}" ## this is for the environment, but you use branch (such as main)
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
  subject             = "repo:${each.value.full_name}:environment:${var.environment_name}" ## this is for the environment, but you use branch (such as main)
}
```
If you've read this far, you might be asking Q: Isn't a User Assigned Identities a bit limiting? You cannot give them access to read Microsoft Graph and therefore they cannot read users, groups or applications, like when trying to authenticate users via easy auth etc...<br>
> [!IMPORTANT]
> Whilst it is *NOT possible* to add Microsoft Graph permissions to an Entra ID Service Principals in the Azure portal, you can done it via the API.
> And, in terraform, you achieve this will the folowing:<br>
## System Assigned Identies - MS Graph permissions
```hcl
data "azuread_application_published_app_ids" "well_known" {}

resource "azuread_service_principal" "msgraph" {
  client_id    = data.azuread_application_published_app_ids.well_known.result.MicrosoftGraph
  use_existing = true
}
data "azuread_service_principal" "msgraph" {
  client_id = data.azuread_application_published_app_ids.well_known.result["MicrosoftGraph"]
}

resource "azuread_app_role_assignment" "sqlserver_system_identity_graph_user_read_all" {
  app_role_id         = data.azuread_service_principal.msgraph.app_role_ids["User.Read.All"]
  principal_object_id = data.azurerm_mssql_server.identity[0].principal_id
  resource_object_id  = data.azuread_service_principal.msgraph.object_id
}
resource "azuread_app_role_assignment" "sqlserver_system_identity_graph_group_read_all" {
  app_role_id         = data.azuread_service_principal.msgraph.app_role_ids["Group.Read.All"]
  principal_object_id = data.azurerm_mssql_server.identity[0].principal_id
  resource_object_id  = data.azuread_service_principal.msgraph.object_id
}
resource "azuread_app_role_assignment" "sqlserver_system_identity_graph_groupmember_read_all" {
  app_role_id         = data.azuread_service_principal.msgraph.app_role_ids["GroupMember.Read.All"]
  principal_object_id = data.azurerm_mssql_server.identity[0].principal_id
  resource_object_id  = data.azuread_service_principal.msgraph.object_id
}
resource "azuread_app_role_assignment" "sqlserver_system_identity_graph_application_read_all" {
  app_role_id         = data.azuread_service_principal.msgraph.app_role_ids["Application.Read.All"]
  principal_object_id = each.value.identity[0].principal_id
  resource_object_id  = data.azuread_service_principal.msgraph.object_id
}
```
For example, you can assigned this system assigned identity of an Azure SQL Server, and then the server can use managed identity to managed access to the database, since the user assigned identity give it enough access to read Entra ID users, group (including group members) and applications. Read more about this [here](https://learn.microsoft.com/en-us/azure/azure-sql/database/authentication-azure-ad-user-assigned-managed-identity?view=azuresql)

but, even better you can use:<br>
## User Assigned Identies - MS Graph permissions
This gives you the ultimate in flexibility as you can apply these permission accross multiple resources, which ultimately requires less code to build and maintain.<br>
```hcl
data "azuread_application_published_app_ids" "well_known" {}

resource "azuread_service_principal" "msgraph" {
  client_id    = data.azuread_application_published_app_ids.well_known.result.MicrosoftGraph
  use_existing = true
}
data "azuread_service_principal" "msgraph" {
  client_id = data.azuread_application_published_app_ids.well_known.result["MicrosoftGraph"]
}

resource "azurerm_user_assigned_identity" "example-identity" {
  name = "id-example-with-graph-permissions"

  resource_group_name = azurerm_resource_group.example.name
  location            = azurerm_resource_group.example.location
  tags                = azurerm_resource_group.example.tags
}
data "azurerm_user_assigned_identity" "example-identity" {
  name                = azurerm_user_assigned_identity.example.name
  resource_group_name = azurerm_user_assigned_identity.example.resource_group_name
}
resource "azuread_app_role_assignment" "github-environment-identity-user-read-all" {
  app_role_id         = data.azuread_service_principal.msgraph.app_role_ids["User.Read.All"]
  principal_object_id = data.azurerm_user_assigned_identity.example.principal_id
  resource_object_id  = data.azuread_service_principal.msgraph.object_id
}
resource "azuread_app_role_assignment" "github-environment-identity-group-read-all" {
  app_role_id         = data.azuread_service_principal.msgraph.app_role_ids["Group.Read.All"]
  principal_object_id = data.azurerm_user_assigned_identity.example.principal_id
  resource_object_id  = data.azuread_service_principal.msgraph.object_id
}
resource "azuread_app_role_assignment" "github-environment-identity-group-member-read-all" {
  app_role_id         = data.azuread_service_principal.msgraph.app_role_ids["GroupMember.Read.All"]
  principal_object_id = data.azurerm_user_assigned_identity.example.principal_id
  resource_object_id  = data.azuread_service_principal.msgraph.object_id
}
resource "azuread_app_role_assignment" "github-environment-identity-group-app-read-all" {
  app_role_id         = data.azuread_service_principal.msgraph.app_role_ids["Application.Read.All"]
  principal_object_id = data.azurerm_user_assigned_identity.example.principal_id
  resource_object_id  = data.azuread_service_principal.msgraph.object_id
}
```

## 📄 Code Snippet

View the full code on Gist:

[![View Gist](https://img.shields.io/badge/View%20Gist-f7792c2f97-blue?logo=github&style=for-the-badge)](https://gist.github.com/webstean/f7792c2f971423591f3efe6bfd450c9a)

<br>
<br>


