---
title: 整合遠端AEM Assets與AEM Sites
description: 瞭解如何在Creative Cloud中透過「已核准的AEM Assets」設定及連線AEM網站。
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# 整合遠端AEM Assets與AEM Sites  {#integrate-approved-assets}

有效管理數位資產對於跨各種線上平台提供吸引人且一致的品牌體驗至關重要。 Dynamic Media搭配OpenAPI功能，可啟用AEM Sites與遠端AEM Assets之間的緊密整合，進而增強數位資產管理。 這項創新功能可讓您輕鬆跨多個AEM環境共用和管理不同型別的已核准數位資產，精簡網站作者和內容編輯的工作流程。

Dynamic Media搭配OpenAPI功能，可讓Sites作者直接在AEM頁面編輯器中使用遠端DAM的資產，並且 [內容片段](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html)，簡化內容建立和管理程式。

使用者可以將多個AEM Sites執行個體（對最大數量沒有任何限制）連線到遠端DAM部署，這是相對於 [連線資產](use-assets-across-connected-assets-instances.md) 功能。

![影像](/help/assets/assets/connected-assets-rdam.png)

初始設定後，使用者可以在AEM Sites執行個體上建立頁面，並視需要新增資產。 新增資產時，他們可以選取儲存在本機DAM中的資產，或瀏覽並使用遠端DAM中可用的資產。

Dynamic Media搭配OpenAPI功能提供數種其他好處，例如存取和使用內容片段中的遠端資產、擷取遠端資產的中繼資料等等。 瞭解更多關於其他的 [Dynamic Media與OpenAPI功能相較於連線資產的優勢](/help/assets/new-dynamic-media-apis-faqs.md).

## 開始之前

* 設定下列專案 [環境變數](/help/implementing/cloud-manager/environment-variables.md#add-variables) AEMas a Cloud Service：

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` 是指方案ID <br>
     `eYYYY` 指環境ID

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]

  或設定 [OSGi設定](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html) 適用於AEM Sites例項中的AEM 6.5，請遵循下列步驟：

   1. 登入主控台並按一下 **[!UICONTROL osgi] >** 或使用直接URL；例如： `http://localhost:4502/system/console/configMgr`

   1. 新增 **[!UICONTROL repositoryID]**= &quot;delivery-pxxxxx-eyyyyyy.adobeaemcloud.com&quot;及 **[!UICONTROL imsClient]**= [IMSClientId]
進一步瞭解 [IMS驗證](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html).

* 以IMS存取登入遠端DAM AEMas a Cloud Service執行個體。

* 在遠端DAM中開啟具有OpenAPI功能的Dynamic Media切換開關。

* 在AEM Sites例項中設定影像v3元件。 如果元件不存在，請下載並安裝 [內容封裝](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## 從遠端DAM存取資產 {#fetch-assets}

Dynamic Media搭配OpenAPI功能，可讓您在本機AEM Sites頁面編輯器和AEM內容片段上存取遠端DAM例項中可用的資產。

![影像](/help/assets/assets/open-APIs.png)

### 在AEM頁面編輯器中存取遠端資產

請依照下列步驟，在您的AEM Sites執行個體上使用AEM頁面編輯器中的遠端資產。 您可以在AEMas a Cloud Service和AEM 6.5中執行這項整合。

1. 前往 **[!UICONTROL 網站]** > _您的網站_ 其中AEM **[!UICONTROL 頁面]** 出現時，您需要新增遠端資產。
1. 導覽至特定的AEM **[!UICONTROL 頁面]** 在您網站內的 **[!UICONTROL 網站]** 您想要新增遠端資產的區段。
1. 選取頁面並按一下 **[!UICONTROL 編輯(_è_)]**. AEM **[!UICONTROL 頁面編輯器]** 隨即開啟。
1. 按一下「版面容器」並新增 **[!UICONTROL 影像]** 元件。
1. 按一下 **[!UICONTROL 影像]** 元件並按一下 ![設定圖示](/help/assets/assets/do-not-localize/settings-icon.svg) 圖示。
1. 取消核取 **[!UICONTROL 從頁面繼承精選影像]** 選項。
1. 按一下 **[!UICONTROL 選取]** 並選取 **[!UICONTROL 遠端]**.
   ![影像](/help/assets/assets/uncheck-inherit-option.jpg)

   系統會提示您登入。
1. 選取資產並按一下 **[!UICONTROL 選取]**.
1. 新增替代文字並按一下 **[!UICONTROL 完成]**.
   <br> 遠端資產會出現在影像元件中。 您也可以在資產載入頁面時，或使用「預覽」索引標籤，驗證資產的傳送URL。 傳遞URL表示資產正由遠端存取。

#### 影片：存取AEM頁面編輯器中的遠端資產

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### 存取AEM內容片段中的遠端資產

請依照下列步驟，在您的AEM Sites執行個體上使用AEM內容片段中的遠端資產。 您可以在AEM 6.5中執行這項整合，但無法在AEMas a Cloud Service上執行。

1. 前往 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]**.
1. 選取出現內容片段的資產資料夾。
1. 選取內容片段並按一下 **[!UICONTROL 編輯(_è_)]**.

   >[!NOTE]
   >
   >如果您沒有AEM內容片段模式，可能需要 [建立一個](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en).

1. 按一下 ![核取記號圖示](/help/assets/assets/do-not-localize/checkmark-icon.svg) 圖示加以存取（位於文字元件旁）。
1. 選取 **[!UICONTROL 遠端]** 從遠端DAM擷取資產。 <br>
您可以選擇 **[!UICONTROL 本機]** 或 **[!UICONTROL 遠端]** DAM存放庫是根據您的需求。

   ![影像](/help/assets/assets/cf-pick.jpg)
系統會提示您登入。
1. 選擇資產並按一下 **[!UICONTROL 選取]**.
   <br> 遠端資產URL會顯示在文字元件中。

#### 影片：存取AEM內容片段中的遠端資產

>[!VIDEO](https://video.tv.adobe.com/v/3427667)
