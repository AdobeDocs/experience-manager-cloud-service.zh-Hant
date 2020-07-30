---
title: 整合 Adobe Target
description: '整合 Adobe Target '
translation-type: tm+mt
source-git-commit: ec747361935b94a729cdd5b6712aee6d3ce1b8a2
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 1%

---


# 整合 Adobe Target{#integrating-with-adobe-target}

Adobe Target是Adobe Marketing Cloud的一部分，可讓您透過跨所有通道的定位和測量，提高內容關聯性。 將Adobe Target和AEM整合為雲端服務需要：

* 使用Touch UI在AEM中建立Analytics設定作為雲端服務（需要IMS設定）。
* 在 [Adobe Launch中新增及設定Adobe Analytics做為擴充功能](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/quick-start.html)。

在AEM頁面（JS程式庫／標籤）中管理Analytics和Target的用戶端屬性時，Adobe Launch是必要的。 儘管如此，Launch需要整合，才能「體驗定位」。 若是「體驗片段」匯出至Target，您只需要Adobe Target設定和IMS。

>[!NOTE]
>
>Adobe Experience Manager是Cloud Service客戶，如果客戶目前沒有Target帳戶，可以要求存取Target Foundation Pack for Experience Cloud。 Foundation Pack提供Target的卷限制使用。

## 建立Adobe Target設定 {#create-configuration}

1. 導覽至「 **工具** 」→ **「雲端服務」**。
   ![導](assets/cloudservice.png "覽")
2. 選取 **Adobe Target**。
3. 選擇「創 **建** 」按鈕。
   ![建立](assets/tenant.png "建立")
4. 填寫詳細資訊（請參閱下面），然後選取「 **Connect**」。
   ![](assets/open_screen.png "ConnectConnect")

### IMS 設定

Launch和Target的IMS設定必須能正確整合Target與AEM和Launch。 雖然Launch的IMS設定已預先設定在AEM中為雲端服務，但必須建立Target IMS設定（在布建Target後）。 請參 [閱此視訊](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html)[和本頁](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html) ，瞭解如何建立Target IMS設定。

### 編輯目標配置 {#edit-target-configuration}

若要編輯Target設定，請依照下列步驟進行：

1. 選擇現有配置，然後按一下「 **屬性」**。
2. 編輯屬性。
3. 選 **取「重新連線至Adobe Target」**。
   ![重新連](assets/edit_config_page.png "接重新連接")
4. Select **Save and Close**.

### 新增設定至網站 {#add-configuration}

若要將Touch UI設定套用至網站，請前往： **Sites** 選擇任何網站頁 **→** Properties **→** Advanced **→ Configuration****** → Select the Configuration tenant。

## 使用Adobe Launch將Adobe Target整合在AEM網站上 {#integrate-target-launch}

AEM提供與Experience Platform Launch的立即可用整合。 借由將Adobe Target擴充功能新增至Experience Platform Launch，您就可以在AEM網頁上使用Adobe Target的功能。Target程式庫僅會使用Launch呈現。

>[!NOTE]
>
>現有（舊版）架構仍然有效，但無法在Touch UI中設定。 建議在Launch中重建變數對應設定。

作為一般概觀，整合步驟包括：

1. 建立啟動屬性
2. 新增所需的擴充功能
3. 建立資料元素（以擷取內容中樞參數）
4. 建立頁面規則
5. 建立和發佈

### 建立啟動屬性 {#create-property}

屬性是一個容器，將填入擴充功能、規則、資料元素。

1. 選擇「新 **建屬性** 」按鈕。
2. 提供您屬性的名稱。
3. 當網域輸入您要載入啟動程式庫的IP/主機時。
4. 選擇「保 **存** 」按鈕。
   ![LaunchpropertyLaunchproperty](assets/properties_newproperty.png "")

### 新增所需的擴充功能 {#add-extension}

**擴充功能** (Extensions)是管理核心程式庫設定的容器。 Adobe Target擴充功能支援用戶端實作，方法是在現代網路上使用Target JavaScript SDK,at.js。 您必須同時新增 **Adobe Target** 和 **** Adobe ContextHub擴充功能。

1. 選取「擴充目錄」選項，並在篩選中搜尋「目標」。
2. 選取 **Adobe Target** at.js，然後按一下「安裝」選項。
   ![Target](assets/search_ext.png "SearchTarget搜尋")
3. 選擇「配 **置** 」按鈕。 請注意，設定視窗中已匯入Target帳戶認證，且此擴充功能的at.js版本已匯入。
4. 選取 **「儲存** 」，將Target擴充功能新增至您的Launch屬性。 您應該可以看到「已安裝的擴充功能」清單下列出 **的Target擴充功能** 。
   ![儲存擴](assets/configure_extension.png "充功能儲存擴充功能")
5. 重複上述步驟以搜尋 **Adobe ContextHub** extension並安裝它（這是與contexthub參數整合時的必要步驟，根據目標設定）。

### 建立資料元素 {#data-element}

**資料元素** ，是您可將上下文中樞參數映射至的預留位置。

1. 選擇 **資料元素**。
2. 選取「 **新增資料元素」**。
3. 提供資料元素的名稱，並將其對應至內容中樞參數。
4. 選擇 **保存**。
   ![資料元](assets/data_elem.png "素資料元素")

### 建立頁面規則 {#page-rule}

在規 **則中** ，我們定義並排序一系列動作，這些動作會在網站上執行，以達成目標。

1. 新增一組動作，如螢幕擷取中所示。
   ![動作](assets/rules.png "動作")
2. 在新增參數至所有Mbox中，將先前設定的資料元素（請參閱上述資料元素）新增至將在mbox呼叫中傳送的參數。
   ![MboxActions](assets/map_data.png "")

### 建立和發佈 {#build-publish}

若要瞭解如何建立和發佈，請參閱本 [頁](https://docs.adobe.com/content/help/en/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html)。

## Classic和Touch UI組態間的內容結構變更 {#changes-content-structure}

| **變更** | **傳統UI配置** | **Touch UI設定** | **後果** |
|---|---|---|---|
| 目標配置的位置。 | /etc/cloudservices/testandtarget/ | /conf/tenant/settings/cloudservices/target | 先前的多個組態都存在於/etc/cloudservices/testandtarget下，但現在單一組態將存在於租用戶下。 |

>[!NOTE]
>
>現有客戶仍支援舊版設定（沒有編輯或建立新設定的選項）。 舊版配置是客戶使用VSTS上傳的內容套件的一部分。
