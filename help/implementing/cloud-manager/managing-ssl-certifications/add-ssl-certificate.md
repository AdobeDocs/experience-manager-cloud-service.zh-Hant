---
title: 新增 SSL 憑證
description: 瞭解如何使用Cloud Manager的自助服務工具新增您自己的SSL憑證或Adobe受管理的DV （網域驗證）憑證。
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 6%

---


# 新增SSL憑證 {#add-ssl-cert}

瞭解如何使用雲端新增您自己的SSL憑證或Adobe受管理的DV （網域驗證）憑證

>[!TIP]
>
>提供憑證可能需要幾天時間。因此，Adobe建議，如果您要提供自己的憑證，建議您在任何期限或上線日期之前提供該憑證。

## 先決條件 {#prerequisites}

* 使用者必須是&#x200B;**企業所有者**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的成員才能新增憑證。
* 如果您正在安裝自己的憑證，請參閱[管理SSL憑證簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)中的&#x200B;**憑證需求**。

## 新增SSL憑證 {#add-certificate}

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登入Cloud Manager並選取適當的程式。
1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。
1. 在頁面的左上角，按一下![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以顯示側邊功能表。
1. 在&#x200B;**服務**&#x200B;標題下，按一下![鎖定已關閉圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL憑證**。

   ![正在新增SSL憑證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. 在[SSL憑證]頁面的右上角附近，按一下[新增SSL憑證]。****

1. 在&#x200B;**新增SSL憑證**&#x200B;對話方塊中，根據[您的特定使用案例](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)，執行下列其中一項作業：

   | | 使用案例 | 步驟 |
   | --- | --- | --- |
   | 1 | **新增Adobe受管理(DV)憑證** | **若要新增Adobe管理的(DV)憑證：**<br> a。在&#x200B;**新增SSL憑證**&#x200B;對話方塊中，選取憑證型別&#x200B;**受管理的Adobe(DV)**。<br>![新增DV憑證](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b。在&#x200B;**憑證名稱**&#x200B;欄位中，輸入您要與憑證關聯的名稱。<br>c。在&#x200B;**選取網域**&#x200B;下拉式清單中，選取一或多個要與DV憑證關聯的網域。<br>沒有要選取的網域？ 若是如此，表示您必須新增自訂網域。 請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。 新增完自訂網域名稱后，請返回本主題並從步驟1重新開始。<br>天。繼續步驟7。 |
   | 2 | **新增客戶管理的(OV/EV)憑證** | **若要新增客戶管理的(OV/EV)憑證：**<br> a。在&#x200B;**新增SSL憑證**&#x200B;對話方塊中，選取憑證型別&#x200B;**客戶管理(OV/EV)**。<br>b。在&#x200B;**憑證名稱**&#x200B;欄位中，輸入憑證的名稱。 此欄位僅供參考，可以是任何有助於您輕鬆引用憑證的名稱。<br>c。在&#x200B;**憑證**、**私密金鑰**&#x200B;和&#x200B;**憑證鏈**&#x200B;欄位中，將必要的值貼到各自的欄位中。<br>![新增SSL憑證對話方塊](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>顯示值中偵測到的任何錯誤。 您必須先解決所有錯誤，才能儲存憑證。 請參閱[憑證錯誤](#certificate-errors)，深入了解疑難排解常見錯誤。<br>天。繼續步驟7。 |

1. 在對話框右下角，按一下「**儲存**」。

成功發行憑證後，**SSL憑證**&#x200B;表格中會顯示綠色核取記號。

您現在已為專案新增有效的SSL憑證。 此步驟通常是第一個設定自訂網域名稱的步驟。

* 若要設定自訂網域名稱，請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。
* 若要瞭解如何在Cloud Manager中更新及管理SSL憑證，請參閱[管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)。

>[!TIP]
>
>如果您在新增或管理憑證時遇到問題，請參閱[疑難排解SSL憑證錯誤](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md)。
