---
layout: post
title:  "Azure ML Automated Deployment - Install AzureMLPS"
date:   2016-07-26 14:08:17 +1000
categories: azureml automation
---

Azure Machine Learning Studio is a web-based GUI for creating machine learning experiments through drag-and-control controls.  This is very useful during the development and testing phase.  On the other hand, if you are looking to deploy existing experiments as part of your build pipeline. then you will need Azure Machine Learning PowerShell (AMLPS). These are the instructions for setting up AMLPS on Windows 10.

- Download and install [Azure PowerShell][azure-ps-releases] v1.5 or higher.  The msi installer is available from GitHub.
- Download [AzureMLPS][azure-mlps] zip file from GitHub.  Extract the files into a temporary folder, the zip should contain a dll file and a template config.json file.
- Replace the values in config.json with the your workspace details (The workspace your experiment will deploy to).  
  * WorkspaceID and AuthorizationToken can be found in the Settings page in AML Studio. 
  * Location is the region the Workspace is provisioned in.
- Move both the dll and modified config.json files to ${AZURE_POWERSHELL_SDK_DIR}\ReasourceManager\AzureResourceManager (e.g. C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ResourceManager\AzureResourceManager)
- Start PowerShell
- Check AzureMLPS module is available in PowerShell using this command:
{% highlight powershell %}
`Get-Module –ListAvailable`
{% endhighlight %}
![Azure ML Screenshot]({{ site.url }}/assets/azure-ml-cmd.png)

Useful commands
----------
-- List all the experiments in the workspace
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
