---
ms.assetid: da7b6dcf-53ec-4394-88c0-c087d92f3893
title: 授權單位的服務管理員範圍
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b5bf2fb3b06a47d730b9dd124b2b66a0a4c9c691
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864849"
---
# <a name="service-administrator-scope-of-authority"></a>授權單位的服務管理員範圍

>適用於：Windows Server 2016 中，Windows Server 2012 R2 中，Windows Server 2012

如果您選擇加入 Active Directory 樹系中，您必須信任樹系擁有者和服務系統管理員。 樹系擁有者負責選擇和管理的服務系統管理員;因此，當您信任的樹系擁有者，您也信任的樹系擁有者管理的服務系統管理員。 這些服務系統管理員會在樹系中的存取權的所有資源。 然後再決定要參與的樹系中，請務必了解樹系擁有者和服務系統管理員將擁有完整存取您的資料。 您無法避免此存取權。  
  
樹系中的所有服務系統管理員會都在樹系中的完整控制所有資料和服務的所有電腦上。 服務系統管理員能夠執行下列作業：  
  
-   請更正錯誤的物件的存取控制清單 (Acl)。 這可讓服務管理員，才能讀取、 修改或刪除物件，不論這些物件設定的 Acl。  
  
-   修改系統軟體，以略過一般安全性檢查網域控制站上。 這可讓服務系統管理員檢視或管理網域中，不論物件上的 ACL 中的任何物件。  
  
-   使用受限群組 」 安全性原則授與給任何使用者或群組系統管理存取權加入網域的任何電腦。 如此一來，服務系統管理員可以取得已加入網域，不論目標電腦擁有者的任何電腦的控制權。  
  
-   重設密碼或變更使用者的群組成員資格。  
  
-   藉由修改網域控制站上的系統軟體存取樹系中其他網域。 服務系統管理員可會影響樹系中，檢視中的任何網域的作業或管理樹系組態資料、 檢視或操作資料儲存在任何網域中，並檢視或操作加入樹系的任何電腦上儲存的資料。  
  
基於這個理由，是儲存在樹系中的組織單位 (Ou) 中的資料，以及將電腦加入到樹系必須信任服務系統管理員的群組。 要加入的樹系的群組，它必須選擇信任樹系中的所有服務系統管理員。 這牽涉到確保：  
  
-   樹系擁有者可以以群組的興趣扮演信任，且沒有對群組執行惡意的動作的原因。  
  
-   樹系擁有者適當限制實體存取網域控制站。 樹系中的網域控制站無法彼此隔離。 可能的攻擊者可以對目錄資料庫，以及透過這種方式進行離線變更、 樹系中，檢視中的任何網域的作業會干擾或操作資料儲存在任何地方的樹系中的單一網域控制站的實體存取並檢視或操作資料儲存在樹系的任何電腦上。 基於這個理由，到網域控制站的實體存取權必須限制為受信任的人員。  
  
-   您會了解，並接受信任的服務系統管理員可以強制轉型為危及系統安全性的潛在風險。  
  
某些群組可能會判斷參與共用的基礎結構的共同作業及降低成本優點勝的風險，服務系統管理員會濫用，或將會強制轉型為誤用其授權單位。 這些群組可以共用樹系，並使用委派權限的 Ou。 不過，其他群組可能不會接受此風險，因為安全性危害的後果是太嚴重。 這些群組需要不同的樹系。  
  

