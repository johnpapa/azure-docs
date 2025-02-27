---
title: Windows 7 virtual machines Azure Virtual Desktop (classic) - Azure
description: How to resolve issues for Windows 7 virtual machines (VMs) in a Azure Virtual Desktop (classic) environment.
author: Heidilohr
ms.topic: troubleshooting
ms.date: 08/08/2022
ms.author: helohr
manager: femila
---
# Troubleshoot Windows 7 virtual machines in Azure Virtual Desktop (classic)

Use this article to troubleshoot issues you're having when configuring the Azure Virtual Desktop session host virtual machines (VMs).

> [!IMPORTANT]
> Azure Virtual Desktop extended support for Windows 7 session host VMs ends on January 10, 2023. To see which operating systems are supported, review [Operating systems and licenses](../prerequisites.md#operating-systems-and-licenses).

## Known issues

Windows 7 on Azure Virtual Desktops doesn't support the following features:

- Virtualized applications (RemoteApps)
- Time zone redirection
- Automatic DPI scaling

Azure Virtual Desktop can only virtualize full desktops for Windows 7.

While Automatic DPI scaling isn't supported, you can manually change the resolution on your virtual machine by right-clicking the icon in the Remote Desktop client and selecting **Resolution**.

## Error: Can't access the Remote Desktop User group

If Azure Virtual Desktop can't find you or your users' credentials in the Remote Desktop User group, you may see one of the following error messages:

- "This user is not a member of the Remote Desktop User group"
- "You must be granted permissions to sign in through Remote Desktop Services"

To fix this error, add the user to the Remote Desktop User group:

1. Open the Azure portal.
2. Select the virtual machine you saw the error message on.
3. Select **Run a command**.
4. Run the following command with `<username>` replaced by the name of the user you want to add:

   ```cmd
   net localgroup "Remote Desktop Users" <username> /add
   ```