This script is for deployment via the [[Azure Releases Pipeline]], via the Azure [[Powershell]] task.

In fact, I think the `Set-AzDiagnosticSetting`  one is the only thing you need. No need for `Remove-AzDiagnosticSetting`. In fact, I was having a lot of issues with it.

```powershell
Write-Host "Starting..."
Write-Host ""

Set-AzDiagnosticSetting -ResourceId "/subscriptions/9b91a2ed-d806-40f2-92ab-e84f03240880/resourceGroups/gc-databricks-workspace-nasa-privatedev-rg/providers/Microsoft.Databricks/workspaces/gc-databricks-workspace-nasa-privatedev-rg" -Name "Testing Databricks Logging PrivDev" -Enabled $False

Write-Host "Disabled DiagnosticSettings..."
Write-Host ""

Remove-AzDiagnosticSetting /subscriptions/9b91a2ed-d806-40f2-92ab-e84f03240880/resourceGroups/gc-databricks-workspace-nasa-privatedev-rg/providers/Microsoft.Databricks/workspaces/gc-databricks-workspace-nasa-privatedev-rg" -Name "Testing Databricks Logging PrivDev"

Write-Host "Deleted DiagnosticSettings..."
Write-Host ""
```

Tags: [[Databricks]], [[DiagnosticSetting]], [[Powershell]], [[Azure]], [[Azure Releases]], [[Azure Pipeline]]