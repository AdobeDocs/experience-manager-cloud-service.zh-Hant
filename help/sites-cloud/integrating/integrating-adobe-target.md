---
title: 整合 Adobe Target
description: 瞭解如何使用觸控式UI和Adobe Launch，將Adobe Target與AEM as a Cloud Service整合。
feature: Integration
role: Admin
exl-id: cf243fb6-5563-427f-a715-8b14fa0b0fc2
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 1%

---

# 整合 Adobe Target{#integrating-with-adobe-target}

Adobe Target是Adobe Experience Cloud的一部分，可讓您透過針對所有管道進行定位和測量，提升內容關聯性。 整合Adobe Target和AEM as a Cloud Service需要：

* 使用Touch UI在AEM as a Cloud Service中建立Target設定（需要IMS設定）。
* 在[Adobe啟動項](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html)中新增並設定Adobe Target為擴充功能。

管理AEM頁面（JS資料庫/標籤）中Analytics和Target的使用者端屬性時，需要Adobe Launch。 也就是說，「體驗鎖定目標」需要與Launch整合。

若要將體驗片段和/或內容片段匯出至Target，您需要[Adobe Target設定](#create-configuration)，包括[IMS整合](#ims-configuration)。

>[!NOTE]
>
>沒有現有Target帳戶的客戶，可要求存取Target Foundation Pack以進行Experience Cloud。 Foundation Pack提供磁碟區有限的Target使用。

## 建立Adobe Target設定 {#create-configuration}

1. 瀏覽至&#x200B;**工具** → **Cloud Service**。
   ![導覽](assets/cloudservice1.png "導覽")
2. 選取&#x200B;**Adobe Target**。
3. 選取&#x200B;**建立**&#x200B;按鈕。
   ![建立](assets/tenant1.png "建立")
4. 填寫詳細資料（請參閱下文），然後選取&#x200B;**連線**。
   ![連線](assets/open_screen1.png "連線")

### IMS 設定 {#ims-configuration}

透過Target Standard API將AEM與Adobe Target整合需要設定Adobe IMS (Identity Management系統)。 必須建立Target IMS設定（布建Target後）。 請參閱[設定AEM as a Cloud Service的IMS整合](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md)和影片[整合Experience Platform Launch和AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)，瞭解如何建立Target IMS設定。

>[!NOTE]
>
>[IMS整合現在已設定為S2S OAuth](/help/security/setting-up-ims-integrations-for-aem-as-a-cloud-service.md)。
>
>先前是使用[JWT認證進行設定，而現在Adobe Developer Console](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)已棄用。

>[!NOTE]
>
>在設定專案時，與一起顯示的產品設定檔取決於您是否擁有：
>
>* Adobe Target Standard — 僅&#x200B;**預設Workspace**&#x200B;可用
>* Adobe Target Premium — 列出所有可用的工作區，如下所示

### Adobe Target租使用者ID和Adobe Target使用者端代碼 {#tenant-client}

設定Adobe Target租使用者ID和Adobe Target使用者端代碼欄位時，請注意下列事項：

1. 對於大多數客戶而言，租使用者ID和使用者端代碼是相同的。 也就是說，兩個欄位包含相同的資訊且相同。 請務必在兩個欄位中輸入租使用者ID。
2. 若是舊版用途，您也可以在「租使用者ID」和「使用者端代碼」欄位中輸入不同的值。

在這兩種情況下：

* 依預設，使用者端代碼（如果先新增）也會自動複製到「租使用者ID」欄位中。
* 如有必要，您可以變更預設的租使用者ID集。
* 對Target進行的後端呼叫是根據租使用者ID，而對Target進行的使用者端呼叫是根據使用者端代碼。

如前所述，第一個案例是AEM as a Cloud Service最常見的情況。 無論是哪一種方式，請根據您的需求，確定&#x200B;**兩個**&#x200B;欄位都包含正確的資訊。

>[!NOTE]
>
> 如果您想要變更現有的Target組態：
>
> 1. 重新輸入租使用者ID。
> 2. 重新連線到Target。
> 3. 儲存設定。

### 編輯Target設定 {#edit-target-configuration}

若要編輯Target設定，請依照下列步驟執行：

1. 選取現有的組態，然後按一下&#x200B;**屬性**。
2. 編輯屬性。
3. 選取&#x200B;**重新連線至Adobe Target**。
4. 選取&#x200B;**儲存並關閉**。

### 將設定新增至站台 {#add-configuration}

若要將Touch UI設定套用至網站，請前往： **網站** > **選取任何網站頁面** > **屬性** > **進階** > **設定** >選取設定租使用者。

## 使用Adobe Launch在AEM網站上整合Adobe Target {#integrate-target-launch}

AEM提供與Experience Platform Launch的現成整合。 將Adobe Target擴充功能新增至Experience Platform Launch後，您就可以在AEM網頁上使用Adobe Target的功能。 Target資料庫僅能使用Launch來呈現。

>[!NOTE]
>
>現有（舊版）架構仍可運作，但無法在Touch UI中設定。 Adobe建議您在Launch中重建變數對應設定。

作為一般概述，整合步驟為：

1. 建立Launch屬性
2. 新增必要的擴充功能
3. 建立資料元素（以擷取內容中樞引數）
4. 建立頁面規則
5. 建置和Publish

### 建立Launch屬性 {#create-property}

屬性是一個內含擴充功能、規則和資料元素的容器。

1. 選取&#x200B;**新增屬性**&#x200B;按鈕。
2. 提供屬性的名稱。
3. 網域請輸入要載入Launch程式庫的IP/主機。
4. 選取&#x200B;**儲存**&#x200B;按鈕。
   ![Launchproperty](assets/properties_newproperty1.png "Launchproperty")

### 新增必要的擴充功能 {#add-extension}

**擴充功能**&#x200B;是管理核心程式庫設定的容器。 Adobe Target擴充功能將Target JavaScript SDK用於現代網路at.js，以支援使用者端實施。 新增&#x200B;**Adobe Target**&#x200B;和&#x200B;**AdobeContextHub**&#x200B;擴充功能。

1. 選取「擴充功能目錄」選項，然後在篩選器中搜尋Target。
2. 選取&#x200B;**Adobe Target** at.js，然後按一下[安裝]選項。
   ![目標搜尋](assets/search_ext1.png "目標搜尋")
3. 選取&#x200B;**設定**&#x200B;按鈕。 請注意已匯入Target帳戶憑證的設定視窗，以及此擴充功能的at.js版本。
4. 選取&#x200B;**儲存**&#x200B;將Target擴充功能新增至您的Launch屬性。 您應該能夠看到&#x200B;**已安裝的擴充功能**&#x200B;清單下列出的Target擴充功能。
   ![儲存擴充功能](assets/configure_extension1.png "儲存擴充功能")
5. 重複上述步驟以搜尋&#x200B;**AdobeContextHub**&#x200B;擴充功能並安裝它（此擴充功能是與ContextHub引數整合的必要專案，視目標定位完成而定）。

### 建立資料元素 {#data-element}

**資料元素**&#x200B;是您可以對應內容中樞引數的預留位置。

1. 選取&#x200B;**資料元素**。
2. 選取&#x200B;**新增資料元素**。
3. 提供資料元素的名稱，並將其對應至內容中心引數。
4. 選取「**儲存**」。
   ![資料元素](assets/data_elem1.png "資料元素")

### 建立頁面規則 {#page-rule}

在&#x200B;**規則**&#x200B;中，它會定義並排序在網站上執行的一系列動作，以達到鎖定目標。

1. 新增一組動作，如熒幕擷圖所示。
   ![動作](assets/rules1.png "動作")
2. 在Add Params to All Mboxes中，將先前設定的資料元素（請參閱上述資料元素）新增至mbox呼叫中傳送的引數。
   ![Mbox](assets/map_data1.png "動作")

### 建置和Publish {#build-publish}

若要瞭解如何建置和發佈，請參閱[頁面](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html)。

## 傳統和觸控式UI設定之間的內容結構變更 {#changes-content-structure}

<table style="table-layout:auto">
  <tr>
    <th>變更</th>
    <th>傳統UI設定</th>
    <th>Touch UI設定</th>
    <th>結果</th>
  </tr>
  <tr>
    <td>Target設定的位置。</td>
    <td>/etc/cloudservices/testandtarget/</td>
    <td>/conf/tenant/settings/cloudconfigs/target/</td>
    <td> 之前，多個設定位於/etc/cloudservices/testandtarget下，但現在單一設定位於租使用者下。</td>
  </tr>
</table>

>[!NOTE]
>
>現有客戶仍支援舊版設定（無法編輯或建立）。 舊版設定是客戶使用VSTS上傳的內容套件的一部分。
