---
title: 整合 Adobe Target
description: '整合 Adobe Target '
feature: Administering
role: Admin
exl-id: cf243fb6-5563-427f-a715-8b14fa0b0fc2
source-git-commit: a2fa676de0d6ca6d7cde3beedd5cc63850966b56
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 1%

---

# 整合 Adobe Target{#integrating-with-adobe-target}

作為Adobe Marketing Cloud的一部分，Adobe Target允許您通過針對所有渠道並進行衡量來提高內容的相關性。 整合Adobe Target和AEMas a Cloud Service需要：

* 使用Touch UI在as a Cloud Service中創AEM建目標配置（需要IMS配置）。
* 添加和配置Adobe Target作為 [Adobe啟動](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html)。

Adobe啟動是管理頁面（JS庫/標籤）中分析和目標的客戶端屬AEM性所必需的。 儘管如此，與Launch的整合對於「經驗目標」是必不可少的。 要導出到目標的體驗片段，您只需要Adobe Target配置和IMS。

>[!NOTE]
>
>Adobe Experience Manager as a Cloud Service客戶如果沒有現有目標帳戶，可以請求訪問Target Foundation Pack以進行Experience Cloud。 Foundation Pack提供了對目標的卷限制使用。

## 建立Adobe Target配置 {#create-configuration}

1. 導航到 **工具** → **Cloud Services**。
   ![導航](assets/cloudservice1.png "導航")
2. 選擇 **Adobe Target**。
3. 選擇 **建立** 按鈕
   ![建立](assets/tenant1.png "建立")
4. 填寫詳細資訊（見下文），然後選擇 **連接**。
   ![連接](assets/open_screen1.png "連接")

### IMS 設定 {#ims-configuration}

為了將目標與發射和發射進行適當整合，需要為發射和目標AEM配置IMS。 雖然啟動的IMS配置在as a Cloud Service中預AEM配置，但必須建立目標IMS配置（在配置目標後）。 請參閱 [這個視頻](https://helpx.adobe.com/experience-manager/kt/sites/using/aem-sites-target-standard-technical-video-understand.html) 和 [此頁](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-ims-adobe-io.html) 瞭解如何建立目標IMS配置。

### Adobe Target租戶ID和Adobe Target客戶端代碼 {#tenant-client}

配置Adobe Target租戶ID和Adobe Target客戶機代碼欄位時，請注意以下事項：

1. 對於大多數客戶，租戶ID和客戶端代碼相同。 這意味著這兩個欄位包含相同的資訊且完全相同。 確保在這兩個欄位中輸入租戶ID。
2. 為了傳統目的，您還可以在「租戶ID」和「客戶端代碼」欄位中輸入不同的值。

在這兩種情況下，請注意：

* 預設情況下，客戶端代碼（如果先添加）也會自動複製到租戶ID欄位中。
* 您可以選擇更改預設租戶ID集。
* 因此，對目標的後端調用將基於租戶ID，而對目標的客戶端調用將基於客戶端代碼。

如前所述，第一個案例是最常見的AEMas a Cloud Service。 不管怎樣，確保 **兩者** 欄位包含的資訊正確，具體取決於您的要求。

>[!NOTE]
>
> 如果要更改現有目標配置：
>
> 1. 重新輸入租戶ID。
> 2. 重新連接到目標。
> 3. 儲存設定。


### 編輯目標配置 {#edit-target-configuration}

要編輯目標配置，請執行以下步驟：

1. 選擇現有配置，然後按一下 **屬性**。
2. 編輯屬性。
3. 選擇 **重新連接到Adobe Target**。
4. 選擇 **保存並關閉**。

### 向站點添加配置 {#add-configuration}

要將Touch UI配置應用到站點，請轉至： **站點** → **選擇任何網站頁** → **屬性** → **高級** → **配置** →選擇配置租戶。

## 利用Adobe Target發AEM布將Adobe整合到現場 {#integrate-target-launch}

提AEM供與Experience Platform Launch的現成整合。 通過將Adobe Target擴展添加到Experience Platform Launch，可以在網頁上使用Adobe TargetAEM的功能。 僅使用「啟動」來呈現目標庫。

>[!NOTE]
>
>現有（舊）框架仍然有效，但無法在Touch UI中配置。 建議在「啟動」中重建變數映射配置。

作為一般概述，整合步驟包括：

1. 建立啟動屬性
2. 添加所需的擴展
3. 建立資料元素（以捕獲上下文中心參數）
4. 建立頁面規則
5. 生成和發佈

### 建立啟動屬性 {#create-property}

屬性是一個容器，其中填充了擴展、規則和資料元素。

1. 選擇 **新建屬性** 按鈕
2. 為您的屬性提供名稱。
3. 作為域，輸入要在其上載入啟動庫的IP/主機。
4. 選擇 **保存** 按鈕
   ![Launchproperty](assets/properties_newproperty1.png "Launchproperty")

### 添加所需的擴展 {#add-extension}

**擴展** 是管理核心庫設定的容器。 Adobe Target擴展支援客戶端實現，方法是使用用於現代Web的目標JavaScript SDK, at.js。 必須同時添加 **Adobe Target** 和 **Adobe上下文中心** 擴展。

1. 選擇「擴展目錄」選項，並在篩選器中搜索「目標」。
2. 選擇 **Adobe Target** at.js ，然後按一下「Install（安裝）」選項。
   ![目標搜索](assets/search_ext1.png "目標搜索")
3. 選擇 **配置** 按鈕 請注意配置窗口，其中導入了目標帳戶憑據，以及此擴展的at.js版本。
4. 選擇 **保存** 將目標擴展添加到啟動屬性。 您應該能夠看到在 **已安裝的擴展** 清單框。
   ![保存擴展](assets/configure_extension1.png "保存擴展")
5. 重複上述步驟以搜索 **Adobe上下文中心** 擴展並安裝它（這是與contexthub參數整合所必需的，根據這些參數將完成目標）。

### 建立資料元素 {#data-element}

**資料元素** 是可將上下文中心參數映射到的佔位符。

1. 選擇 **資料元素**。
2. 選擇 **添加資料元素**。
3. 提供資料元素的名稱並將其映射到上下文中心參數。
4. 選擇 **保存**。
   ![資料元素](assets/data_elem1.png "資料元素")

### 建立頁面規則 {#page-rule}

在 **規則** 我們定義並排序一系列在現場執行的動作，以實現目標。

1. 添加一組操作，如螢幕抓圖中所示。
   ![操作](assets/rules1.png "操作")
2. 在「將參數添加到所有框」中，將先前配置的資料元素（請參閱上面的資料元素）添加到將在框調用中發送的參數中。
   ![框](assets/map_data1.png "操作")

### 生成和發佈 {#build-publish}

要瞭解如何生成和發佈，請參閱此 [頁](https://experienceleague.adobe.com/docs/experience-manager-learn/aem-target-tutorial/aem-target-implementation/using-launch-adobe-io.html)。

## Classic和Touch UI配置之間的內容結構更改 {#changes-content-structure}

<table style="table-layout:auto">
  <tr>
    <th>更改</th>
    <th>經典UI配置</th>
    <th>觸摸UI配置</th>
    <th>後果</th>
  </tr>
  <tr>
    <td>目標配置的位置。</td>
    <td>/etc/cloudservices/testandtarget/</td>
    <td>/conf/tenant/settings/cloudservices/target/</td>
    <td> 以前在/etc/cloudservices/testandtarget下存在多個配置，但現在在租戶下存在單個配置。</td>
  </tr>
</table>

>[!NOTE]
>
>現有客戶仍支援舊式配置（沒有編輯或建立新配置的選項）。 舊式配置將是客戶使用VSTS上傳的內容包的一部分。
