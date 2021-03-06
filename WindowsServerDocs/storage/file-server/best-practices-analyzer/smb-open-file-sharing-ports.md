---
title: SMB-檔案和印表機共用埠應開啟
ms.date: 07/02/2012
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: dc2e1d7f5408ad123297b8df2dc06f59053fe870
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954765"
---
# <a name="smb-file-and-printer-sharing-ports-should-be-open"></a>SMB：檔案和印表機共用連接埠應該開啟


已更新：2011年2月2日

適用于： Windows Server 2019、Windows Server 2016、Windows Server 2012 R2 和 Windows Server 2012、Windows Server 2008 R2

*本主題旨在解決最佳做法分析程式掃描所識別的特定問題。本主題中的資訊僅適用于已對其執行「檔案服務」最佳做法分析程式並遇到本主題所解決之問題的電腦。如需最佳做法和掃描的詳細資訊，請參閱*[最佳做法分析](https://go.microsoft.com/fwlink/?linkid=122786%0d%0a)程式。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>作業系統</strong></p></td>
<td><p>Windows Server</p></td>
</tr>
<tr class="even">
<td><p><strong>產品/功能</strong></p></td>
<td><p>檔案服務</p></td>
</tr>
<tr class="odd">
<td><p><strong>嚴重性</strong></p></td>
<td><p>錯誤</p></td>
</tr>
<tr class="even">
<td><p><strong>類別</strong></p></td>
<td><p>組態</p></td>
</tr>
</tbody>
</table>

## <a name="issue"></a>問題

> *檔案及印表機共用所需的防火牆埠未開啟 (埠445和 139) 。*

## <a name="impact"></a>影響

> *電腦將無法存取此伺服器上 (SMB) 型網路服務的共用資料夾和其他伺服器訊息區。*

## <a name="resolution"></a>解決方法

> *啟用 [檔案及印表機共用] 以透過電腦的防火牆進行通訊。*

您至少必須有 **Administrators** 群組的成員資格或同等權限，才能完成此程序。

## <a name="to-open-the-firewall-ports-to-enable-file-and-printer-sharing"></a>若要開啟防火牆埠以啟用檔案及印表機共用

1.  開啟 [控制台]，按一下 [**系統及安全性**]，然後按一下 [ **Windows 防火牆**]。

2.  在左窗格中，按一下 [ **Advanced settings**]，然後在主控台樹中，按一下 [**輸入規則**]。

3.  在 [**輸入規則**] 底下，找出 [規則] [檔案**和印表機共用 (]-[會話) ** ] 和 [檔案**及印表機共用] ([SMB-in) **]。

4.  針對每個規則，以滑鼠右鍵按一下該規則，然後按一下 [啟用規則]****。

## <a name="additional-references"></a>其他參考資料

[瞭解共用資料夾與 Windows 防火牆](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731402(v=ws.11)) (https://technet.microsoft.com/library/cc731402.aspx)
