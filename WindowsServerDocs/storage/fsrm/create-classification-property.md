---
title: 建立分類屬性
description: 本文說明用於指派值給指定之資料夾或磁碟區中檔案的分類屬性。
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 8a5d044ae78ad45b59fa4cb97694c15aad3c4bbe
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957495"
---
# <a name="create-a-classification-property"></a>建立分類屬性

> 適用於：Windows Server (半年度管道)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

分類屬性可用來將值指派給指定之資料夾或磁碟區中的檔案。 視您的需要而定，有許多屬性類型可以從中選擇。 下表定義可用的屬性類型。

|屬性 | 描述 |
| --- | --- |
| 是/否 | 可以為 **\[是\]** 或 **\[否\]** 的布林值屬性。 在分類期間或在檔案內容中合併多個值時，**\[是\]** 值會覆寫 **\[否\]** 值。 |
| 日期時間 | 簡單的日期/時間屬性。 在分類期間或在檔案內容中合併多個值時，衝突的值將會阻止重新分類。 |
| Number | 簡單的數字屬性。 在分類期間或在檔案內容中合併多個值時，衝突的值將會阻止重新分類。 |
| 排序清單 | 固定值的清單。 一次只能指派一個值給屬性。 在分類期間或在檔案內容中合併多個值時，將會使用清單中最高的值。 |
| String | 簡單的字串屬性。 在分類期間或在檔案內容中合併多個值時，衝突的值將會阻止重新分類。 |
| 複選 | 可指派給屬性的值清單。 一次可以指派多個值給屬性。 在分類期間或在檔案內容中合併多個值時，將會使用清單中的每個值。 |
| 多字串 | 可指派給屬性的字串清單。 一次可以指派多個值給屬性。 在分類期間或在檔案內容中合併多個值時，將會使用清單中的每個值。 |

<br />

下列程序會引導您完成建立分類屬性的流程。

## <a name="to-create-a-classification-property"></a>若要建立分類屬性

1.  按一下 **\[分類管理\]** 中的 **\[分類屬性\]** 節點。

2.  在 **\[分類屬性\]** 上按滑鼠右鍵，再按一下 **\[建立屬性\]** (或按一下 **\[動作\]** 窗格中的 **\[建立屬性\]**)。 如此會開啟 **\[分類屬性定義\]** 對話方塊。

3.  在 **\[屬性名稱\]** 文字方塊中，輸入屬性的名稱。

4.  在 **\[描述\]** 文字方塊中，加入屬性的選用描述。

5.  在 **\[屬性類型]** 下拉式功能表中，從清單選取屬性類型。

6.  按一下 [確定]  。

## <a name="additional-references"></a>其他參考資料

-   [建立自動分類規則](create-automatic-classification-rule.md)
-   [分類管理](classification-management.md)