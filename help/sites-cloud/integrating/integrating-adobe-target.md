---
title: 整合 Adobe Target
description: '整合 Adobe Target '
feature: 管理
role: Admin
exl-id: cf243fb6-5563-427f-a715-8b14fa0b0fc2
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 1%

---

# 整合 Adobe Target{#integrating-with-adobe-target}

作為Adobe Marketing Cloud的一部分，Adobe Target可讓您透過鎖定目標並測量所有管道，來提升內容相關性。 將Adobe Target和AEM整合為Cloud Service需要：

* 使用觸控式UI在AEM中建立Target設定作為Cloud Service（需要IMS設定）。
* 在[AdobeLaunch](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/quick-start.html)中新增並設定Adobe Target為擴充功能。

AdobeLaunch是管理AEM頁面（JS程式庫/標籤）中Analytics和Target的用戶端屬性的必要。 也就是說，「體驗鎖定目標」需要與Launch整合。 若要將體驗片段匯出至Target，您只需要Adobe Target設定和IMS。

>[!NOTE]
>
>Adobe Experience Manager作為沒有現有Target帳戶的Cloud Service客戶，可以要求存取Target Foundation Pack以進行Experience Cloud。 Foundation Pack提供對Target的卷有限使用。

## 建立Adobe Target設定 {#create-configuration}

1. 導覽至&#x200B;**工具** → **Cloud Services**。
   ![](assets/cloudservice1.png "導覽導覽")
2. 選擇&#x200B;**Adobe Target**。
3. 選擇&#x200B;**Create**按鈕。
   ![](assets/tenant1.png "CreateCreate")
4. 填寫詳細資訊（請參閱下面），然後選擇&#x200B;**Connect**。
   ![](assets/open_screen1.png "ConnectConnect")

### IMS 設定 {#ims-configuration}

若要正確整合Target與AEM和Launch,Launch和Target的IMS設定是必要的。 雖然AEM中的Launch IMS設定已預先設定為Cloud Service，但必須建立Target IMS設定（布建Target後）。 請參閱[此影片](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html)和[本頁面](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-ims-adobe-io.html)以了解如何建立Target IMS設定。

### Adobe Target租用戶ID和Adobe Target用戶端代碼 {#tenant-client}

設定Adobe Target租用戶ID和Adobe Target用戶端代碼欄位時，請注意下列事項：

1. 對於大部分的客戶，租用戶ID和用戶端代碼都相同。 這表示兩個欄位包含相同的資訊，且相同。 請務必在兩個欄位中輸入租用戶ID。
2. 為了傳統用途，您也可以在租用戶ID和用戶端代碼欄位中輸入不同的值。

在這兩種情況下，請注意：

* 依預設，用戶端代碼（若是先新增的）也會自動複製到租用戶ID欄位中。
* 您可以選擇變更預設的租用戶ID集。
* 因此，對Target的後端呼叫將以租用戶ID為基礎，而對Target的用戶端呼叫將以用戶端代碼為基礎。

如前所述，第一個案例是AEM as aCloud Service最常見的案例。 無論是哪種方式，請根據您的需求，確定&#x200B;**兩個**&#x200B;欄位皆包含正確的資訊。

>[!NOTE]
>
> 如果要變更現有的Target設定：
>
> 1. 重新輸入租用戶ID。
> 2. 重新連線至Target。
> 3. 儲存設定。


### 編輯目標配置 {#edit-target-configuration}

若要編輯Target設定，請依照下列步驟操作：

1. 選擇現有配置，然後按一下&#x200B;**屬性**。
2. 編輯屬性。
3. 選擇&#x200B;**重新連接到Adobe Target**。
4. 選擇&#x200B;**保存並關閉**。

### 將配置添加到站點 {#add-configuration}

若要將觸控式UI設定套用至網站，請前往：**Sites** → **選擇任何站點頁面** → **屬性** → **Advanced** → **Configuration** →選擇配置租戶。

## 使用Launch整合AEM網站上的Adobe Target {#integrate-target-launch}

AEM提供立即可用的與Experience Platform Launch整合。 將Adobe Target擴充功能新增至Experience Platform Launch後，您就可以在AEM網頁上使用Adobe Target的功能。 Target程式庫只能透過Launch來轉譯。

>[!NOTE]
>
>現有（舊版）架構仍可運作，但無法在觸控式UI中設定。 建議您在Launch中重建變數對應設定。

整合步驟為：

1. 建立Launch屬性
2. 新增所需的擴充功能
3. 建立資料元素（以擷取內容中樞參數）
4. 建立頁面規則
5. 建置和發佈

### 建立Launch屬性 {#create-property}

屬性是一個容器，裡面裝滿擴充功能、規則、資料元素。

1. 選擇&#x200B;**新屬性**&#x200B;按鈕。
2. 提供屬性的名稱。
3. 以網域的形式，輸入要載入launch程式庫的IP/主機。
4. 選擇&#x200B;**保存**按鈕。
   ![](assets/properties_newproperty1.png "LaunchpropertyLaunchproperty")

### 新增所需的擴充功能 {#add-extension}

**** 擴充管理核心程式庫設定的容器。Adobe Target擴充功能可在現代網路at.js中使用Target JavaScript SDK來支援用戶端實作。 您必須同時新增&#x200B;**Adobe Target**&#x200B;和&#x200B;**AdobeContextHub**&#x200B;擴充功能。

1. 選取擴充功能目錄選項，然後在篩選器中搜尋Target。
2. 選取&#x200B;**Adobe Target** at.js ，然後按一下安裝選項。
   ![目標](assets/search_ext1.png "搜尋目標搜尋")
3. 選擇&#x200B;**配置**&#x200B;按鈕。 請注意已匯入Target帳戶憑證的設定視窗，以及此擴充功能的at.js版本。
4. 選取&#x200B;**儲存**，將Target擴充功能新增至您的Launch屬性。 您應該可以在&#x200B;**已安裝擴充功能**清單下看到列出的Target擴充功能。
   ![儲存擴充](assets/configure_extension1.png "功能儲存擴充功能")
5. 重複上述步驟以搜尋&#x200B;**AdobeContextHub**&#x200B;擴充功能並加以安裝（這是與ContextHub參數整合的必要項目，且會根據該參數進行定位）。

### 建立資料元素 {#data-element}

**資** 料元素是可將內容中樞參數對應到的預留位置。

1. 選擇&#x200B;**資料元素**。
2. 選擇&#x200B;**添加資料元素**。
3. 提供資料元素的名稱，並將其對應至內容中樞參數。
4. 選擇&#x200B;**保存**。
   ![資料](assets/data_elem1.png "元素資料元素")

### 建立頁面規則 {#page-rule}

在&#x200B;**Rule**&#x200B;中，我們定義並排序在網站上執行的動作序列，以達成鎖定目標。

1. 新增一組動作，如螢幕擷取所示。
   ![](assets/rules1.png "動作動作")
2. 在新增參數至所有mbox中，將先前設定的資料元素（請參閱上述資料元素）新增至將在mbox呼叫中傳送的參數。
   ![](assets/map_data1.png "MboxActions")

### 建置和發佈 {#build-publish}

若要了解如何建立和發佈，請參閱此[page](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html)。

## 傳統版和觸控式UI組態之間的內容結構變更 {#changes-content-structure}

| **變更** | **傳統UI配置** | **觸控式UI設定** | **後果** |
|---|---|---|---|
| 目標配置的位置。 | /etc/cloudservices/testandtarget/ | /conf/tenant/settings/cloudservices/target | 先前的/etc/cloudservices/testandtarget下有多個設定，但現在租用戶下有單一設定。 |

>[!NOTE]
>
>現有客戶仍支援舊式設定（無法編輯或建立新設定）。 舊版設定是使用VSTS之客戶上傳的內容套件的一部分。
