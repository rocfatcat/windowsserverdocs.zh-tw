---
title: DirectAccess 不支援的設定
description: 本主題提供 Windows Server 2016 中不支援的 DirectAccess 設定清單。
manager: brianlic
ms.topic: article
ms.assetid: 23d05e61-95c3-4e70-aa83-b9a8cae92304
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 6d10b0bcef354bc1746d05d212d47f836d9c28c2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951293"
---
# <a name="directaccess-unsupported-configurations"></a>DirectAccess 不支援的設定

>適用於：Windows Server (半年度管道)、Windows Server 2016

開始部署之前，請先參閱下列不支援的 DirectAccess 設定清單，以避免再次啟動部署。

## <a name="file-replication-service-frs-distribution-of-group-policy-objects-sysvol-replications"></a><a name="bkmk_frs"></a>檔案複寫服務 (FRS) 散發群組原則物件 (SYSVOL 複製) 
請勿在網域控制站執行檔案複寫服務的環境中部署 DirectAccess， (FRS) 以散發群組原則物件 (SYSVOL 複寫) 。 當您使用 FRS 時，不支援部署 DirectAccess。

如果您有執行 Windows Server 2003 或 Windows Server 2003 R2 的網域控制站，則會使用 FRS。 此外，如果您先前使用的是 Windows 2000 Server 或 Windows Server 2003 網域控制站，而且從未將 SYSVOL 複寫從 FRS 遷移至分散式檔案系統複寫 (的) ，則您可能會使用 FRS。

如果您使用 FRS SYSVOL 複寫部署 DirectAccess，您會有風險地刪除 DirectAccess 群組原則物件，其中包含 DirectAccess 伺服器和用戶端設定資訊。 如果刪除這些物件，您的 DirectAccess 部署將會遭遇中斷，而使用 DirectAccess 的用戶端電腦將無法連線到您的網路。

如果您打算部署 DirectAccess，您必須使用執行作業系統的網域控制站，而不是 Windows Server 2003 R2，而且您必須使用 DFS-R。

如需從 FRS 遷移至 DFS-R 的相關資訊，請參閱[SYSVOL 複寫遷移指南： FRS to DFS 複寫](../../../storage/dfs-replication/migrate-sysvol-to-dfsr.md)。

## <a name="network-access-protection-for-directaccess-clients"></a><a name="bkmk_nap"></a>DirectAccess 用戶端的網路存取保護
網路存取保護 (NAP) 用來判斷遠端用戶端電腦是否符合 IT 原則，然後才會授與公司網路的存取權。 Windows Server 2012 R2 中的 NAP 已淘汰，不包含在 Windows Server 2016 中。 基於這個理由，不建議使用 NAP 來啟動新的 DirectAccess 部署。 建議針對 DirectAccess 用戶端的安全性使用不同的端點控制方法。

## <a name="multisite-support-for-windows-7-clients"></a><a name="bkmk_multi"></a>Windows 7 用戶端的多網站支援
在多網站部署中設定 DirectAccess 時，Windows 10 &reg; 、windows &reg; 8.1 和 windows &reg; 8 用戶端都可以連接到最接近的網站。  Windows 7 &reg; 用戶端電腦沒有相同的功能。 Windows 7 用戶端的網站選擇會在原則設定時設為特定網站，而且這些用戶端一律會連線到該指定的網站，而不論其位置為何。

## <a name="user-based-access-control"></a><a name="bkmk_user"></a>以使用者為基礎的存取控制
DirectAccess 原則是以電腦為基礎，而不是以使用者為基礎。 不支援指定 DirectAccess 使用者原則來控制對公司網路的存取。

## <a name="customizing-directaccess-policy"></a><a name="bkmk_policy"></a>自訂 DirectAccess 原則
您可以使用 DirectAccess 安裝程式、[遠端存取管理] 主控台或 [遠端存取] Windows PowerShell Cmdlet 來設定 DirectAccess。 不支援使用 DirectAccess 設定向導以外的任何方式來設定 DirectAccess，例如直接修改 DirectAccess 群組原則物件，或手動修改伺服器或用戶端上的預設原則設定。 這些修改可能會導致無法使用的設定。

## <a name="kerbproxy-authentication"></a><a name="bkmk_kerb"></a>KerbProxy authentication
當您使用消費者入門 Wizard 設定 DirectAccess 伺服器時，DirectAccess 伺服器會自動設定為使用 KerbProxy authentication 進行電腦和使用者驗證。 因此，您應該只將消費者入門 Wizard 用於僅部署 Windows 10 &reg; 、Windows 8.1 或 windows 8 用戶端的單一網站部署。

此外，下列功能不應該與 KerbProxy authentication 搭配使用：

-   使用外部負載平衡器或 Windows Load Balancer 來進行負載平衡

-   需要使用智慧卡或一次性密碼 (OTP) 的雙因素驗證

如果您啟用 KerbProxy authentication，則不支援下列部署方案：

-   網站.

-   Windows 7 用戶端的 DirectAccess 支援。

-   強制通道。 為確保當您使用強制通道時，不會啟用 KerbProxy authentication，請在執行嚮導時設定下列專案：

    -   啟用強制通道

    -   為 Windows 7 用戶端啟用 DirectAccess

> [!NOTE]
> 針對先前的部署，您應該使用 [Advanced Configuration Wizard]，它會使用兩個通道的設定搭配以憑證為基礎的電腦和使用者驗證。 如需詳細資訊，請參閱[使用 Advanced Settings 部署單一 DirectAccess 伺服器](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)。

## <a name="using-isatap"></a><a name="bkmk_isa"></a>使用 ISATAP
ISATAP 是一種轉換技術，可在僅 IPv4 的公司網路中提供 IPv6 連線能力。 它僅限於具有單一 DirectAccess 伺服器部署的中小型組織，並可讓您從遠端系統管理 DirectAccess 用戶端。 如果 ISATAP deployedin 為多網站、負載平衡或多重網域環境，您必須先將它移除，或將它移至原生 IPv6 部署，然後再設定 DirectAccess。

## <a name="iphttps-and-one-time-password-otp-endpoint-configuration"></a><a name="bkmk_iphttps"></a> (OTP) 端點設定的 IPHTTPS 和一次性密碼
當您使用 IPHTTPS 時，IPHTTPS 連線必須在 DirectAccess 伺服器上終止，而不是在任何其他裝置（例如負載平衡器）上結束。 同樣地，頻外安全通訊端層 (在單次密碼期間建立的 SSL) 連線 (OTP) 驗證必須在 DirectAccess 伺服器上終止。 這些連線的端點之間的所有裝置都必須以傳遞模式設定。

## <a name="force-tunnel-with-otp-authentication"></a><a name="bkmk_ft"></a>使用 OTP 驗證強制通道
請勿使用 OTP 和強制通道的雙因素驗證來部署 DirectAccess 伺服器，否則 OTP 驗證將會失敗。 DirectAccess 伺服器和 DirectAccess 用戶端之間必須有頻外安全通訊端層 (SSL) 連線。 此連線需要豁免，才能在 DirectAccess 通道外傳送流量。 在強制通道設定中，所有流量都必須流經 DirectAccess 通道，而且在建立通道之後，不允許豁免。 因此，不支援在強制通道設定中使用 OTP 驗證。

## <a name="deploying-directaccess-with-a-read-only-domain-controller"></a><a name="bkmk_rodc"></a>使用唯讀網域控制站部署 DirectAccess
DirectAccess 伺服器必須具有讀寫網域控制站的存取權，而且無法在唯讀網域控制站 (RODC) 中正常運作。

有許多原因需要讀寫網域控制站，包括下列各項：

-   在 DirectAccess 伺服器上，需要讀寫網域控制站，才能開啟遠端存取 Microsoft Management Console (MMC) 。

-   DirectAccess 伺服器必須讀取和寫入 DirectAccess 用戶端和 DirectAccess 伺服器，群組原則物件 (Gpo) 。

-   DirectAccess 伺服器會從 (PDCe) 的主域控制站模擬器，特別讀取及寫入用戶端 GPO。

基於這些需求，請勿使用 RODC 部署 DirectAccess。

