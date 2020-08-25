---
layout: post
title:  "Installing AD DS on Windows Server"
date:   2020-08-24 12:20:00 -0400
categories: IT reference
---

## Installing AD DS on Server 2012

# Prerequisites
- NTFS partition with Server 2012  
- DNS installed and configured     
   - Forward and Reverse lookup zones
   - Dynamic updates (properties > Dynamic Updates > Nonsecure and secure dropdown)  
- Static IP  
- Change DNS suffix to point to the new AD namespace and restart  

# Install AD Binaries
- Server manager > Manage > Add roles and features  
- Installation Type: Role-based or feature-based installation  
- Select the Server  
- Server Roles: Active Directory Domain Services (also installs RSAT)  

# Promote to a Domain Controller
DC promo only works on Server Core post 2012; you will be redirected to server manager.  
Notifications > Post-deployment configuration > "Promote this server..."  
If this is the first DC in the entire AD infrastructure, select "Add a new forest" otherwise use the first option.  
At the "Review Options" tab, you can select "View script" to see the powershell cmdlets needed to execute the options you selected.  
Install > Restart > Sign in as Domain Admin using DOMAIN\USERNAME  

# IFM Install
Used for a second server in a remote location to copy ntds.dit and /sysvol  
Faster than pulling everything over the Internet  

**On the secondary DC**
Set a static IP and have DNS point to the primary DC
Create a new dir on C:/ and share
Install AD binaries
Join to the domain

**On the primary DC**
Map the shared folder from the secondary dc
Create a copy of the AD database (NTDS.DIT) and SYSVOL directory
```
admin cmd > ntdsutil
ntdsutil: activate instance ntds
ntdsutil: ifm
ifm: create sysvol full <mapped drive path to shared folder>
```

**On the secondary server**
Promote to DC
Deselect DNS and GC
Under additional options > Select the domain controller to replicate from and select the checkbox "Install from media"
Select the path: C:\IFM and Verify

# Upgrading a DC
```
ADPrep /forestprep  
ADPrep /domainprep  
```
