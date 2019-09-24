# AzureAutomation.HybridWorker
Onboarding script for unattended hybrid worker installation

## Powershell script to onboard new machines as Hybrid Worker for Azure Automation
> Note: The Azure Automation Account and the Azure Log Analytics workspace must be in the same region

> Note: Following scripts applies to Windows VMs only

```powershell
#Install the Log Analytics Agent on the VM, and register the VM in an Hybrid Worker group for an Azure Automation Account
$hybridWorkerGroupName = "myGroup"
$workspaceId = "<WorkspaceId>"
$workspaceKey = "<WorkspaceKey>"
$automationAccountEndpoint = "<AutomationAccountUrl>"
$automationAccountKey = "<AutomationAccountPrimaryKey>"

./hybridworker.ps1 -HybridGroupName "$hybridWorkerGroupName" -WorkspaceId "$workspaceId" -WorkspaceKey $workspaceKey -AutomationAccountEndpoint "$automationAccountEndpoint" -AutomationAccountKey "$automationAccountKey"
```

## Onboard Windows VMs using  CustomScriptExtension
```powershell
#Install the Log Analytics Agent on the VM, and register the VM in an Hybrid Worker group for an Azure Automation Account
#Uses CustomScriptExtension to deploy the unattended installation script
$vmName = "<VmName>"
$vmRgName = "<VmResourceGroups>"
$vmLocation = "<VmLocation>"
$scriptUri = "https://raw.githubusercontent.com/rbickel/AzureAutomation.HybridWorker/master/hybridworker.ps1"
$hybridWorkerGroupName = "myGroup"
$workspaceId = "<WorkspaceId>"
$workspaceKey = "<WorkspaceKey>"
$automationAccountEndpoint = "<AutomationAccountUrl>"
$automationAccountKey = "<AutomationAccountPrimaryKey>"

$settings =  @{
    CommandToExecute = "powershell -ExecutionPolicy Unrestricted -File hybridworker.ps1 -HybridGroupName '$hybridWorkerGroupName' -WorkspaceId '$workspaceId' -WorkspaceKey '$workspaceKey' -AutomationAccountKey '$automationAccountKey' -AutomationAccountEndpoint '$automationAccountEndpoint'"
    fileUris = @("$scriptUri")
    timestamp = Get-Random
 }

Set-AzVMExtension -ResourceGroupName $vmRgName `
    -Location $vmLocation `
    -VMName $vmName `
    -Name "AAHybridWorker" `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion "1.9" `
    -Settings $settings
```
