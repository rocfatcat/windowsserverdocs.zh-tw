---
title: 角色、 角色服務和功能不在 Server Core 容器-Windows Server 版本 1803
description: 深入了解我們已移除 Windows Server 的 Server Core 容器映像的功能與角色。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 05/07/2018
ms.openlocfilehash: 0ad574a04ba7ecd235f1825bd25c247a1565edf6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873779"
---
# <a name="roles-role-services-and-features-not-in-server-core-containers---windows-server-version-1803"></a>角色、 角色服務和功能不在 Server Core 容器-Windows Server 版本 1803

> 適用於：Windows Server 版本 1803

在 Windows Server，版本 1803，我們已[降低整體的 Server Core 容器映像大小**1.58 GB**](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/)。 接下來的方式是藉由最佳化的架構和移除項目中您不需要[Server Core 容器](https://docs.microsoft.com/virtualization/windowscontainers/about/)。 有些在容器中的，不能用於項目，有些角色及功能沒有人使用。 

> [!IMPORTANT]
> 我們已移除從 Server Core**容器**映像，不[本身的 Server Core](server-core-roles-and-services.md)。 

以下是從 Server Core 容器映像中移除的角色功能的完整清單：

<div style='font-size:9.0pt'>

<br>ADCertificateServicesRole
<br>AuthManager
<br>Bitlocker-Utilities
<br>BitLocker
<br>BITS
<br>BITSExtensions-Upload
<br>CCFFilter
<br>CertificateEnrollmentPolicyServer
<br>CertificateEnrollmentServer
<br>CertificateServices
<br>ClientForNFS-Infrastructure
<br>容器
<br>CoreFileServer
<br>DataCenterBridging-LLDP-Tools
<br>DataCenterBridging
<br>重複資料刪除-核心
<br>DeviceHealthAttestationService
<br>DFSN-Server
<br>DFSR-Infrastructure-ServerEdition
<br>DirectoryServices-ADAM
<br>DirectoryServices-DomainController
<br>DiskIo-QoS
<br>EnhancedStorage
<br>FailoverCluster-AdminPak
<br>FailoverCluster-AutomationServer
<br>FailoverCluster-CmdInterface
<br>FailoverCluster-FullServer
<br>FailoverCluster-PowerShell
<br>File-Services
<br>FileServerVSSAgent
<br>FRS-Infrastructure
<br>FSRM-Infrastructure-Services
<br>FSRM-Infrastructure
<br>HardenedFabricEncryptionTask
<br>HostGuardian
<br>HostGuardianService-Package
<br>IdentityServer-SecurityTokenService
<br>IPAMClientFeature
<br>IPAMServerFeature
<br>iSCSITargetServer-PowerShell
<br>iSCSITargetServer
<br>iSCSITargetStorageProviders
<br>iSNS_Service
<br>授權
<br>LightweightServer
<br>Microsoft-Hyper-V-Management-Clients
<br>Microsoft-Hyper-V-Offline
<br>Microsoft-Hyper-V-Online
<br>Microsoft-Hyper-V
<br>Microsoft-Windows-FCI-Client-Package
<br>Microsoft-Windows-GroupPolicy-ServerAdminTools-Update
<br>Microsoft-Windows-Subsystem-Linux
<br>MSRDC-Infrastructure
<br>MultipathIo
<br>NetworkController
<br>NetworkControllerTools
<br>NetworkDeviceEnrollmentServices
<br>NetworkLoadBalancingFullServer
<br>NetworkVirtualization
<br>OnlineRevocationServices
<br>P2P-PnrpOnly
<br>PeerDist
<br>Printing-Client-Gui
<br>Printing-LPDPrintService
<br>Printing-Server-Foundation-Features
<br>列印伺服器角色
<br>QWAVE
<br>RasRoutingProtocols
<br>Remote-Desktop-Services
<br>RemoteAccess
<br>RemoteAccessMgmtTools
<br>RemoteAccessPowerShell
<br>RemoteAccessServer
<br>ResumeKeyFilter
<br>RightsManagementServices-Role
<br>RightsManagementServices
<br>RMS-Federation
<br>SBMgr-UI
<br>ServerCore-Drivers-General-WOW64
<br>ServerCore-Drivers-General
<br>ServerForNFS-Infrastructure
<br>ServerManager-Core-RSAT-Feature-Tools
<br>ServerMediaFoundation
<br>ServerMigration
<br>SessionDirectory
<br>SetupAndBootEventCollection
<br>ShieldedVMToolsAdminPack
<br>SMB1Protocol-Server
<br>SmbDirect
<br>SMBHashGeneration
<br>SmbWitness
<br>SNMP
<br>SoftwareLoadBalancer
<br>Storage-Replica-AdminPack
<br>Storage-Replica
<br>Tpm-PSH-Cmdlets
<br>UpdateServices-Database
<br>UpdateServices-Services
<br>UpdateServices-WidDatabase
<br>UpdateServices
<br>VmHostAgent
<br>VolumeActivation-Full-Role
<br>Web-Application-Proxy
<br>WebAccess
<br>WebEnrollmentServices
<br>Windows-Defender
<br>WindowsServerBackup
<br>WindowsStorageManagementService
<br>WINSRuntime
<br>WMISnmpProvider
<br>WorkFolders-Server
<br>WSS-Product-Package

</div>