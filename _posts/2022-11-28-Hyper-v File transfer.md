---
title: Hyper-V File Transfer with virtual Machines
date: 2022-11-28 14:00:00 +0000
categories: [Hyper-V]
tags: [hyper-v, virtual machines, file transfer, powershell direct, guest services]     # TAG names should always be lowercase
---


# Hyper-V File Transfer with virtual Machines

Copying Files between Virtual Machines running on a Hyper-V and that are isolated from the network can be tricky. This post describes, how files can be directly transferred by using powershell and Guest additions.

  
## Enable Guest Additions

Hyper-V Manager -> VM -> Settings -> Integration Services -> Guest Services -> enable

or by running the following Powershell Command:
```
Enable-VMIntegrationService -Name 'Guest Service Interface' –VMName <VMName>
```


## Copy File from and to Machines
### Copy with Copy-VMFile

Copy-VMFile only allows copying to a VM and not from a VM.

```
Copy-VMFile -Name "VM-NAME" -SourcePath "C:\temp\filestocopy" –DestinationPath 'C:\destinationFolder\destinationFileName' -FileSource Host –CreateFullPath
```


## Copy File from Virtual Machine with Powershell Direct


```
$VM = "VMName"
$Session = New-PSSession -VMName $VM -Credential "~\Administrator"
Enter-PSSession -Session $Session
[VMName]: PS C:\Users\Administrator\Documents> dir
[VMNAME]: PS C:\Users\Administrator\Documents> Exit
```

### Copy File to Session:
```
Copy-Item -ToSession $Session -Path C:\SourceFile.txt -Destination D:\DestinationFile.txt
```

### Copy File from Session:
```
Copy-Item -FromSession $Session -Path D:\SourceFile.txt -Destination C:\DestinationFile.txt
Get-ChildItem C:\Host\