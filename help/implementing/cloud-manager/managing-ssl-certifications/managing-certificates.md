---
title: 管理 SSL 憑證
description: 了解如何使用 Cloud Manager 檢查 SSL 憑證的狀態以及如何編輯、取代、更新和刪除它們。
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 13%

---


# 管理 SSL 憑證 {#managing-ssl-certificates}

了解如何使用 Cloud Manager 檢查 SSL 憑證的狀態以及如何編輯、取代、更新和刪除它們。

## 檢查SSL憑證的狀態 {#checking-status-an-ssl-certificate}

Cloud Manager會提供程式中所有憑證狀態的概觀。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的方案。
1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。
1. 在頁面的左上角，按一下![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以顯示側邊功能表。
1. 在&#x200B;**服務**&#x200B;標題下，按一下![鎖定已關閉圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL憑證**。

**SSL憑證**&#x200B;頁面會提供您SSL憑證的狀態。

| SSL憑證的狀態 | 說明 |
| --- | --- |
| 綠色 | 憑證從目前日期起至少14天有效。 |
| 橙色 | 憑證將在14天內到期。<br>·確定您有更新憑證的計畫，並透過Cloud Manager使用者介面取代憑證，以避免可能的網站存取或中斷。<br>· Cloud Manager會在UI中定期傳送通知，提醒您憑證即將到期。 |
| 紅色 | SSL憑證已過期。<br>請參閱[更新過期的客戶管理的SSL憑證](#update-ssl-certificate)或[刪除SSL憑證](#deleting-an-ssl-certificate)。 |

## 更新過期的客戶管理的SSL憑證 {#update-ssl-certificate}

當客戶管理的憑證過期時，與過期憑證一起使用的任何網域都將不再運作。 更新憑證可確保您的網域繼續如期運作。

使用者必須是&#x200B;**企業所有者**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的成員才能完成此工作。

>[!IMPORTANT]
>
>新增或更新SSL憑證時，請勿在憑證鏈結中包含新憑證。 如果包含此引數，上傳將無法成功完成。

**若要更新已過期的客戶管理的SSL憑證：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的方案。
1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。
1. 在頁面的左上角，按一下![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以顯示側邊功能表。
1. 在&#x200B;**服務**&#x200B;標題下，按一下![鎖定已關閉圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL憑證**。
1. 在您要更新的過期客戶管理憑證列中，按一下最右邊的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後按一下&#x200B;**檢視和更新**。

   ![更新過期的客戶管理的SSL認證](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. 在&#x200B;**檢視和更新SSL憑證**&#x200B;對話方塊中，執行下列動作：

   * （選擇性）在&#x200B;**憑證名稱**&#x200B;欄位中，輸入新名稱。
   * 在&#x200B;**憑證**&#x200B;欄位貼上新的憑證內容金鑰。
   * 在&#x200B;**私密金鑰**&#x200B;欄位中，只有在您變更憑證時才更新此欄位。
   * 在&#x200B;**憑證鏈**&#x200B;欄位（或信任鏈）貼上憑證鏈。

1. 按一下&#x200B;**更新**&#x200B;以儲存變更並自動套用變更。


>[!NOTE]
>
>如果有兩個或更多SAN憑證涵蓋相同的SAN網域專案，且其中一個憑證已更新，則系統會為網域安裝更新的憑證。
>
>如需詳細資訊，請參閱[疑難排解SSL憑證問題](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md#wrong-san-cert)。

## 取代過期的客戶管理的SSL憑證 {#replace-ssl-certificate}

請依照[更新過期的SSL憑證](#update-ssl-certificate)中所述的相同步驟操作，以取代過期的客戶管理的SSL憑證。

## 重新命名Adobe管理的SSL憑證(#rename-an-ssl-certificate)

以下是可能需要重新命名SSL憑證的幾個原因：

* **已改善組織**：重新命名憑證可協助釐清其用途，例如識別其適用的環境（例如，測試、生產）或網域。
* **避免混淆**：如果您正在管理多個憑證，使用清楚的描述性名稱有助於避免發生錯誤，例如將錯誤的憑證套用至錯誤的網域。
* **法規遵循與稽核**：為了安全性和稽核目的，較容易追蹤正確命名的憑證。

**若要重新命名Adobe管理的SSL憑證：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的方案。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 在頁面的左上角，按一下![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以顯示側邊功能表。

1. 在&#x200B;**服務**&#x200B;標題下，按一下![鎖定已關閉圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL憑證**。

1. 在&#x200B;**SSL憑證**&#x200B;頁面上，按一下資料列結尾的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，該資料列的&#x200B;**Adobe已管理**&#x200B;您要重新命名的SSL憑證。

1. 在下拉式功能表中，按一下&#x200B;**重新命名**。

1. 在&#x200B;**重新命名DV憑證**&#x200B;對話方塊的&#x200B;**憑證名稱**&#x200B;文字欄位中，輸入憑證的新名稱。

1. 按一下「**重新命名**」。


## 刪除SSL憑證 {#deleting-an-ssl-certificate}

從Cloud Manager中刪除Adobe Managed或客戶管理的SSL憑證是無法復原的永久性動作。 作為最佳實務，Adobe建議您先在本機儲存SSL檔案，然後再在Cloud Manager中刪除它們。

>[!NOTE]
>
>您無法刪除與一或多個使用中網域相關聯的Adobe管理的SSL憑證。 在刪除SSL憑證之前，必須刪除所有關聯的使用中網域。 請參閱[管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)以瞭解更多資訊。

使用者必須是&#x200B;**企業所有者**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的成員才能完成此工作。

**若要刪除SSL憑證：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的方案。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 在頁面的左上角，按一下![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以顯示側邊功能表。

1. 在&#x200B;**服務**&#x200B;標題下，按一下![鎖定已關閉圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL憑證**。

1. 在「SSL憑證」頁面上，在您要刪除之憑證的表格列中，按一下最右邊的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後按一下&#x200B;**刪除**。

   如果&#x200B;**Delete**&#x200B;有資訊圖示（如下列影像所示），請參閱上述附註。

   ![刪除含有資訊圖示的按鈕](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. 在&#x200B;**刪除SSL憑證**&#x200B;對話方塊中，按一下&#x200B;**刪除**&#x200B;以確認刪除。

1. 執行管道以取消部署已刪除的憑證。


## 既有的CDN設定 {#pre-existing-cdn}

如果您已有SSL憑證的CDN設定，**SSL憑證**&#x200B;頁面會顯示資訊訊息。 我們建議您透過UI新增這些設定，以便在Cloud Manager中檢視及管理這些設定。

使用UI移轉所有預先存在的環境設定後，該訊息就會消失。 訊息可能需要一到兩個營業日才能消失。

如需詳細資訊，請參閱[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。

對於具有IP允許清單或自訂網域名稱的既有CDN設定的環境，**IP允許清單**&#x200B;和&#x200B;**環境**&#x200B;頁面上也提供了類似的訊息。
