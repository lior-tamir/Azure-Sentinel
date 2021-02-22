# Cisco ASA - Add or remove IP Addresses from a Network Object Group

## Summary

This playbook allows blocking/allowing of IPs in Cisco ASA, using a **Network Object Group**. This allows making changes to a Network Object Group members, instead of making Access Control Entries. The Network Object Group itself should be part of an Access Control Entry.

When a new Sentinel incident is created,this playbook gets triggered and performs below actions
1. For the IPs we check if the are already a member of the Network Object Group
2. An adaptive card is sent to a Teams channel with information about the incident and giving the option to ignore an IP, or depdening on it's current status block it by adding it to the Network Object Group or unblock it by removing it from the Network Object Group

### Prerequisites
1. **This playbook template is based on Azure Sentinel Incident Trigger which is currently in Private Preview (Automation Rules).** You can change the trigger to the Sentinel Alert trigger in cases you are not part of the Private Preview.
2. Cisco ASA custom connector needs to be deployed prior to the deployment of this playbook, in the same resource group. Relevant instructions can be found in the connector doc page.
3. In Cisco ASA there needs to be a Network Object Group. 

### Deployment instructions 
1. Deploy the playbook by clicking on "Depoly to Azure" button. This will take you to deplyoing an ARM Template wizard.

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Flaurens1984%2FAzure-Sentinel%2Ffeature%2FCiscoASAConnector%2FPlaybooks%2FCiscoASAConnector%2FCiscoASA-AddIPtoNetworkObjectGroup%2Fazuredeploy.json" target="_blank">
    <img src="https://aka.ms/deploytoazurebutton"/>
</a>

<a href="https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Flaurens1984%2FAzure-Sentinel%2Ffeature%2FCiscoASAConnector%2FPlaybooks%2FCiscoASAConnector%2FCiscoASA-AddIPtoNetworkObjectGroup%2Fazuredeploy.json" target="_blank">
   <img src="https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazuregov.png"/>    
</a>

2. Fill in the required paramteres:
    * Playbook Name: Enter the playbook name here (ex:CiscoASA-AddIPtoNetworkObjectGroup)
    * Teams GroupId : Enter the Teams channel id to send the adaptive card
    * Teams ChannelId : Enter the Teams Group id to send the adaptive card
    [Refer the below link to get the channel id and group id](https://docs.microsoft.com/en-us/powershell/module/teams/get-teamchannel?view=teams-ps)
    * Cisco ASA Connector name : Enter the name of the Cisco ASA custom connector (default value:CiscoASAConnector)

### Post-Deployment instructions 
#### a. Authorize connections
Once deployment is complete, you will need to authorize each connection.
1.	Click the Azure Sentinel connection resource
2.	Click edit API connection
3.	Click Authorize
4.	Sign in
5.	Click Save
6.	Repeat steps for other connections such as Teams and Cisco ASA (For authorizing the Cisco ASA API connection, the username and password needs to be provided)

#### b. Configurations in Sentinel
1. In Azure sentinel analytical rules should be configured to trigger an incident with IP Entity.
2. Configure the automation rules to trigger this playbook
