---
title: 新增自訂網域名稱
description: 了解如何使用 Cloud Manager 新增自訂網域名稱。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 27%

---


# 新增自訂網域名稱 {#adding-cdn}

了解如何使用 Cloud Manager 新增自訂網域名稱。

## 要求 {#requirements}

在Cloud Manager中新增自訂網域名稱之前，請先滿足這些要求。

* 在新增自訂網域名稱（如檔案[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)中所述）之前，您必須為要新增的網域新增網域SSL憑證。
* 您必須擁有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色，才能在Cloud Manager中新增自訂網域名稱。
* 正在使用Fastly CDN。

## 新增自訂網域名稱的位置 {#where}

您可以從 Cloud Manager 中的兩個位置新增自訂網域名稱：

* [從域設定頁面](#adding-cdn-settings)
* [從環境頁面](#adding-cdn-environments)

新增自訂網域名稱時，會使用最明確的有效憑證提供網域。 如果多個憑證具有相同的網域，則選擇最近更新的憑證。 Adobe建議您管理憑證，以免網域重疊。

本檔案中描述的步驟是以Fastly為基礎。 如果您使用不同的CDN，請使用您選擇要使用的CDN來設定網域。

## 從網域設定頁面新增自訂網域名稱 {#adding-cdn-settings}

按照以下步驟從&#x200B;**域設定**&#x200B;頁。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 導覽至左側導覽面板中的選取&#x200B;**網域設定**&#x200B;索引標籤。

   ![域設定窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 按一下右上角的&#x200B;**新增網域**&#x200B;按鈕以開啟&#x200B;**新增網域名稱**&#x200B;對話方塊。

   ![新增網域對話方塊](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 在&#x200B;**網域名稱**&#x200B;索引標籤上，在&#x200B;**網域名稱**&#x200B;欄位中輸入自訂網域名稱。

   >[!NOTE]
   >
   >不包括`http://`,`https://`, 或輸入您的域時的空格。

1. 選擇&#x200B;**環境**&#x200B;其服務與網域名稱相關聯。

1. 選擇任一&#x200B;**發布**&#x200B;或者&#x200B;**預習**&#x200B;服務。

1. 選擇&#x200B;**網域 SSL 憑證**&#x200B;從下拉清單中與網域名稱關聯並選擇&#x200B;**繼續**。

1. **驗證**&#x200B;標籤出現。

   ![網域名稱識別](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   * **驗證**&#x200B;索引標籤說明設定自訂網域名稱的後續步驟，這會建立必要的TXT記錄。
   * 您可以立即執行此步驟（在按一下對話方塊中的&#x200B;**建立**&#x200B;之前），或在按一下對話方塊中的&#x200B;**建立**&#x200B;之後。
   * 選項和後續步驟如下所述。

1. 按一下&#x200B;**建立**&#x200B;以在Cloud Manager中儲存自訂網域名稱。

當您在&#x200B;**新增自訂網域**&#x200B;精靈中選取&#x200B;**建立**&#x200B;時，Cloud Manager會觸發TXT驗證。 當您在Cloud Manager中設定自訂網域名稱時，請建立TXT記錄。 不過，不需要執行此步驟。 對於後續驗證，您必須主動選取狀態旁邊的&#x200B;**再次驗證**&#x200B;圖示。

在Cloud Manager驗證是否已新增及驗證TXT專案之前，該名稱不會啟用。 **已驗證和部署**&#x200B;的狀態表示成功的TXT驗證。

* 請參閱[新增TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)以進一步瞭解TXT記錄。
* 請參閱[檢查網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)，以瞭解Cloud Manager如何驗證自訂網域名稱及其TXT專案的詳細資訊。

## 後續步驟 {#next-steps}

在Cloud Manager中建立自訂網域名稱后，請新增TXT專案以驗證網域的所有權。 繼續檔案[新增TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)以繼續設定您的自訂網域名稱。

## 從環境頁面 {#adding-cdn-environments}

從&#x200B;**環境**&#x200B;頁面新增自訂網域名稱的步驟與[從「網域設定」頁面](#adding-cdn-settings)新增自訂網域名稱的步驟相同，但進入點不同。 按照以下步驟從&#x200B;**環境**&#x200B;頁面。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 瀏覽至感興趣環境的&#x200B;**環境詳細資料**&#x200B;頁面。

   ![在環境詳情頁面輸入網域名稱](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用&#x200B;**網站網域名稱**&#x200B;表提交自訂網域名稱。

   1. 輸入自訂網域名稱。
   1. 從下拉清單中選擇與此名稱關聯的 SSL 憑證。
   1. 按一下&#x200B;**+新增**。

   ![新增自訂網域名稱](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. **新增網域名稱**&#x200B;對話方塊會開啟至&#x200B;**網域名稱**&#x200B;索引標籤。 繼續進行，如同從[網域設定]頁面](#adding-cdn-settings)新增自訂網域名稱一樣。[
