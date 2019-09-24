# AzureAutomation.HybridWorker
Onboarding script for unattended hybrid worker installation

## Powershell script to onboard new machines as Hybrid Worker for Azure Automation
> Note: The Azure Automation Account and the Azure Log Analytics workspace must be in the same region

```powershell
#Install a new hybrid worker on a VM and register it to the target Azure Automazion Account
$hybridWorkerGroupName = "myGroup"
$workspaceId = "62b7bb25-7bfa-4006-bffc-a1c8667e37f6"
$workspaceKey = "HxxiiaHH292+np3rrG03qIFGoqiJL1pdn/fHagV+VwFsqfQxstL5Pt+RuVM1goWyA9CbxZMiJChhF6IgKaphGQ=="
$automationAccountEndpoint = "https://we-agentservice-prod-1.azure-automation.net/accounts/121d7ffa-30e3-41df-a028-d96a1c4f3f63"
$automationAccountKey = "+OAZg2eFUSWPDssfKSQ/9pNoodShYP0yh3MQG7m83zbGUG5VjW5pjIfZBndYNfBNLsndiHYQLlyjkrmhgyE8eg="

./hybridworker.ps1 -HybridGroupName $hybridWorkerGroupName -WorkspaceId $workspaceId -WorkspaceKey $workspaceKey -AutomationAccountEndpoint $automationAccountKey -AutomationAccountKey $automationAccountKey
```

## Onboard machines using the CustomScriptExtension
```powershell
#Install a new hybrid worker on a VM and register it to the target Azure Automazion Account
$hybridWorkerGroupName = "myGroup"
$workspaceId = "62b7bb25-7bfa-4006-bffc-a1c8667e37f6"
$workspaceKey = "HxxiiaHH292+np3rrG03qIFGoqiJL1pdn/fHagV+VwFsqfQxstL5Pt+RuVM1goWyA9CbxZMiJChhF6IgKaphGQ=="
$automationAccountEndpoint = "https://we-agentservice-prod-1.azure-automation.net/accounts/121d7ffa-30e3-41df-a028-d96a1c4f3f63"
$automationAccountKey = "+OAZg2eFUSWPDssfKSQ/9pNoodShYP0yh3MQG7m83zbGUG5VjW5pjIfZBndYNfBNLsndiHYQLlyjkrmhgyE8eg="

./hybridworker.ps1 -HybridGroupName $hybridWorkerGroupName -WorkspaceId $workspaceId -WorkspaceKey $workspaceKey -AutomationAccountEndpoint $automationAccountKey -AutomationAccountKey $automationAccountKey
```