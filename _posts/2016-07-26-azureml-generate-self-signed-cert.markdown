---
layout: post
title:  "Azure ML Automated Deployment - Generate Self-Signed Certificate"
date:   2016-07-26 14:08:17 +1000
categories: azureml automation
---

To execute the *List-AmlWorkspaces* and *New-AmlWorkspace*, the Azure Management must have a copy of the certificate to authorize automation command access from only certain machines.
For testing purposes, you can generate a self-signed certificate using [makecert.exe][makecert].

**How to install makecert in Windows 7:**

- Download and install Windows SDK, you only need to select .NET Development Tools when choosing the component to install
- Add SDK bin directory to PATH, e.g. the SDK bin directory is likely to be C:\Program Files\Microsoft SDKs\Windows\v7.x\Bin
- Start PowerShell and run makecert to generate the certificate:
{% highlight powershell %}
makecert.exe -sky exchange -r -n 'CN={CERTIFICATE_NAME}' -pe -a sha1 -len 2048 -ss My 'MyAzureMgmtCert.cer'
{% endhighlight %}
${CERTIFICATE_NAME} will be the name of the certificate that appears as the certificate name in Azure certificate store, so choose a name that you can associate the certificate with this machine.

Run this command to show the thumbprint of the generated certificate:
{% highlight powershell %}
(dir Cert:\CurrentUser\My | where Subject -eq 'CN={CERTIFICATE_NAME}').Thumbprint
{% endhighlight %}
For Windows 8 or later, you can use the PowerShell command [New-SelfSignedCertificate] [ps-self-signed-cert] instead for generating the certificate.

[ps-self-signed-cert]: http://www.mistercloudtech.com/2015/12/17/how-to-create-a-custom-self-signed-certificate-with-powershell/
[makecert]: https://msdn.microsoft.com/en-us/library/ms733813(v=vs.110).aspx
