```powershell
$vmssRgName = "Automation"
$vmssName = "AAHybridWorker2"

$vmss = Get-AzVmss -ResourceGroupName $vmssRgName -VMScaleSetName $vmssName
Add-AzVmssExtension `
    -VirtualMachineScaleSet $vmss `
    -Name "AAHybridWorker" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion "1.9" `
    -ProtectedSetting $settings

#Remove-AzVmssExtension -VirtualMachineScaleSet $vmss -Name "AAHybridWorker"
Update-AzVmss -ResourceGroupName $vmssRgName -Name $vmssName -VirtualMachineScaleSet $vmss

#$settings = $settings | ConvertTo-Json -Compress  | % { [System.Text.RegularExpressions.Regex]::Unescape($_) } 
#$protectedSettings = $protectedSettings | ConvertTo-Json -Compress  | % { [System.Text.RegularExpressions.Regex]::Unescape($_) } 
az vmss extension set  `
  --publisher "Microsoft.Compute" `
  --version 1.9 `
  --name "CustomScriptExtension" `
  --extension-instance-name "AAHybridWorker" `
  --force-update `
  --resource-group $vmssRgName `
  --vmss-name $vmssName `
  --settings $settings `
  --protected-settings $settings
```