---
title: 從 Windows Server 版本 1903 開始移除或計劃取代的功能
description: 以下清單列出的 Windows Server 1903 版特性與功能已從該版本的產品中移除，或開始考慮可能在後續版本中取代。 適用對象是在商業環境中更新作業系統的 IT 專業人員。
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
ms.date: 10/15/2019
author: jasongerend
ms.author: jgerend
manager: daveba
ms.openlocfilehash: b72f75509e9a50477bb1857782ef5dd4e2670b3f
ms.sourcegitcommit: b9ec35416a06854c1bc875a2b731d42a436fe313
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/12/2019
ms.locfileid: "73956117"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1903-and-1909"></a>從 Windows Server 版本 1903 和 1909 開始移除或計劃取代的功能

>適用於：Windows Server 版本 1903 和 1909

以下清單列出的 Windows Server 版本 1903 和 1909 特性與功能已從該版本的產品中移除，或開始考慮可能在後續版本中取代。 適用對象是在商業環境中更新作業系統的 IT 專業人員。 **此清單的後續版本可能會變更，並非所有受影響的特色或功能都包含在其中。**

另請參閱 [Windows Server 中已移除或計劃取代的功能](removed-features.md)。

## <a name="features-were-no-longer-developing"></a>我們不再開發的功能

我們不再主動開發這些功能，而且可能在未來更新中加以移除。 有些功能已取代為其他特色或功能，有些則暫時從不同的來源提供。 

如果您有建議取代任何這些功能的意見反應要分享，可以使用[意見反應中樞 App](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)。 


|                         功能                         |                                                                                                                                                                                                                                                                                                                                                                                                                           您可以改用                                                                                                                                                                                                                                                                                                                                                                                                                            |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              LBFO 上的 Hyper-V vSwitch                |                                                                                                                                                                  在未來版本中，Hyper-V vSwitch 將不再具有繫結至 LBFO 小組的功能。 相反地，它必須透過 [交換器內嵌小組 (SET)](../virtualization/hyper-v-virtual-switch/rdma-and-switch-embedded-teaming.md#switch-embedded-teaming-set) 加以繫結。                                                                                                                                                                    |
|       XDDM 型遠端顯示驅動程式 (**新增**)        |                                                                                                                                          從此版本開始，遠端桌面服務會針對單一工作階段的遠端桌面，使用以 Windows 顯示驅動程式模型 (WDDM) 為基礎的間接顯示驅動程式 (IDD)。 未來版本中將移除以 Windows 2000 顯示驅動程式模型 (XDDM) 為基礎的遠端顯示驅動程式支援。 獨立軟體廠商若使用以 XDDM 為基礎的遠端顯示驅動程式，則應開始計畫遷移至 WDDM 驅動程式模型。 若要深入了解如何實作遠端顯示的間接顯示驅動程式 ISV，請連絡 [rdsdev@microsoft.com](mailto:rdsdev@microsoft.com)。                                                                                                                                           |
|            UCS 記錄收集工具 (**新增**)            |                                                                                                                                                                                                                                                                                                                                                         雖然 UCS 記錄收集工具並非明確地用於 Windows Server，但仍由 Windows 10 上的意見反應中樞所取代。                                                                                                                                                                                                                                                                                                                                                         |
|              Hyper-V 中的金鑰存放磁碟機               |                                                                                                                                                                                                        Hyper-V 中將不再使用金鑰存放磁碟機功能。 如果您使用第 1 代 VM，請參閱[第 1 代 VM 虛擬化安全性](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/generation-1-virtual-machine-security-settings-for-hyper-v)，以了解之後的相關資訊。 如果您要建立新的 VM，請使用搭配 TPM 裝置的第 2 代虛擬機器，以取得更安全的解決方案。                                                                                                                                                                                                         |
|    信賴平台模組 (TPM) 管理主控台     |                                                                                                                                                                                                                          先前在 TPM 管理主控台中提供的資訊，現在也可以在 [Windows Defender 資訊安全中心](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/windows-defender-security-center)的[**裝置安全性**](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/wdsc-device-security)頁面取得。                                                                                                                                                                                                                          |
| 主機守護者服務的 Active Directory 證明模式 | 我們已不再開發主機守護者服務的 Active Directory 證明模式 - 相反地，我們已新增新的證明模式：[主機金鑰證明](../security/guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md)，這是最簡單且同樣與 Active Directory 相容的證明。  此新模式提供具有安裝體驗的同等功能，比起 Active Directory 證明，其管理方式更簡單，基礎結構相依性也較少。 主機金鑰證明的硬體需求皆沒有超過 Active Directory 證明所要求的內容，因此所有現有系統仍可與新的模式相容。 請參閱[部署受防護主機](../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)，取得有關證明選項的相關資訊。 |
|                     OneSync 服務                     |                                                                                                                                                                                                                                                                                                                                                   OneSync 服務可同步郵件、行事曆和人員應用程式的資料。 我們已將同步引擎新增至 Outlook 應用程式以提供相同的同步功能。                                                                                                                                                                                                                                                                                                                                                    |
|       遠端差異壓縮 API 支援       |                                                                                                                                                                                                                                                                                                           遠端差異壓縮 API 支援可使用壓縮技術 (將網路間傳送的資料最小化) 來同步資料與遠端來源。 |
|         WFP 輕量型篩選器的交換器擴充功能         |                                                                                                                                                                                                                                      WFP 輕量型篩選器的交換器擴充功能可讓開發人員[針對 Hyper-V 虛擬交換器建置簡單的網路封包篩選擴充功能](https://docs.microsoft.com/windows-hardware/drivers/network/using-virtual-switch-filtering)。 您可以建立完整的篩選擴充功能來達到相同功能性。 因此，我們將在未來移除此擴充功能。                                                                                                                                                                                                                                      |

