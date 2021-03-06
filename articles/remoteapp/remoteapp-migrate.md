---
title: Migrate user data from Azure RemoteApp | Microsoft Docs
description: Learn how to migrate your user data in and out of Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin

ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin

---
# How to migrate data into and out of Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp is being discontinued on August 31, 2017. Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.
> 
> 

You can use many different tools and methods to transfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp. Here are a few methods:

* Copy and paste using clipboard sharing
* Copy files and data to a file server
* Copy files to OneDrive for Business through a browser
* Copy files using redirection

> [!NOTE]
> You cannot enable the OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.
> 
> 

## Use copy and paste in File Explorer
Copy and paste using the clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md). This lets users copy files between their local PC and RemoteApp apps. Often, through the normal course of using apps in RemoteApp, users have saved files to their UPDs - moving that data out of RemoteApp is easy:

1. [Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection. (Note that this is an administrative task.)
2. Direct your users to launch the File Explorer app you published and to use that to copy and paste files both into their UPD and out of it.

## Upload files and data to a file server by using standard network file copy
Often organizations use file servers to store general data. If you know the server name or location, your users can browse the local network for the server and then copy their files there, much like they did above. Again you'll want to publish File Explorer to RemoteApp and then share it with your users.

> [!NOTE]
> The file server must be on the routable network that RemoteApp was deployed into.
> 
> 

## Copy files to OneDrive for Business
Although you cannot enable the OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD to OneDrive for Business through a browser. 

1. Publish File Explorer to RemoteApp and then tell users to access the files through that app. 
2. It's easiest to transfer files if they are compressed, so users should create a .zip file that contains all of the files to move to OneDrive for Business.
3. Ask users to go to the Office 365 portal, and then go to OneDrive and upload the .zip file.

## Copy files by using drive redirection
If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users. In this case, they can zip their files on the redirected drive and then save them to their local PC.

## How administrators can export data

Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription to Azure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.  There is no ability to select individual UPD's.  When the PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported to Azure storage.  Costs of Azure storage will incur immediately for this storage.  When running this command ensure there are no sessions otherwise the export will fail.

UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.  If these disks will be used in an RDS deployment we recommend to use our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import the UPD's into an RDS deployment.

