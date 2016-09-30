---
layout: post
title:  "Azure ML Automated Deployment - Install AzureMLPS"
date:   2016-07-26 14:08:17 +1000
categories: azureml automation
---

- Download and install [Azure PowerShell][azure-ps-releases] v1.5 or higher
- Download [AzureMLPS module v0.8.2][azure-mlps].  Extract the 2 files inside the zip file into a temporary folder.
- Replace the values in config.json with the correct workspace details.  The workspace ID and workspace token can be found in Azure ML Studio (under settings). The location is the region the Workspace is provisioned in.
- Move the files to ${AZURE_POWERSHELL_SDK_DIR}\ReasourceManager\AzureResourceManager, e.g. C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ResourceManager\AzureResourceManager
- Start PowerShell
- Check AzureMLPS module is available in PowerShell:
{% highlight powershell %}
Get-Module –ListAvailable
{% endhighlight %}
![Azure ML Screenshot]({{ site.url }}/assets/azure-ml-cmd.png)

- You can now run commands for accessing or modifying workspace resources by linking to the config.json file that contains the workspace authorization details, 
e.g. List all the experiments in the workspace
{% highlight powershell %}
Get-AmlExperiment -ConfigFile {CONFIG_FILE_DIR}\config.json
{% endhighlight %}
For all the available AMLPS commands, refer to the [azuremlps README] [azuremlps-readme] on GitHub.

> To find out what parameters are supported for a commandlet, use the *Get-Help* command, e.g. 
{% highlight powershell %}
 Get-Help Get-AmlWorkspace
{% endhighlight %}


[azure-ps-releases]: https://github.com/Azure/azure-powershell/releases
[azure-mlps]:   https://github.com/hning86/azuremlps/releases
[azuremlps-readme]: https://github.com/hning86/azuremlps
