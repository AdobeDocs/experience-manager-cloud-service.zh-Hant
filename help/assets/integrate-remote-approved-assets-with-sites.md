---
title: 將遠端 AEM Assets 與 AEM Sites 整合
description: 瞭解如何在Creative Cloud中透過「已核准的AEM Assets」設定及連線AEM網站。
source-git-commit: f6c0e8e5c1d7391011ccad5aa2bad4a6ab7d10c3
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 2%

---


# 將遠端 AEM Assets 與 AEM Sites 整合  {#integrate-approved-assets}

有效管理數位資產對於跨各種線上平台提供吸引人且一致的品牌體驗至關重要。 Dynamic Media搭配OpenAPI功能，可啟用AEM Sites與AEM Assetsas a Cloud Service之間的緊密整合，進而增強數位資產管理。 這項創新功能可讓您輕鬆跨多個AEM環境共用和管理不同型別的已核准數位資產，精簡網站作者和內容編輯的工作流程。

透過OpenAPI功能的Dynamic Media，Sites作者可直接在AEM頁面編輯器和[內容片段](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html)中使用遠端DAM的資產，藉此簡化內容建立和管理程式。

使用者可以將多個AEM Sites執行個體（對最大數量沒有任何限制）連線到遠端DAM部署，這是優於[連線的Assets](use-assets-across-connected-assets-instances.md)功能的顯著優點。

![影像](/help/assets/assets/connected-assets-rdam.png)

初始設定後，使用者可以在AEM Sites執行個體上建立頁面，並視需要新增資產。 新增資產時，他們可以選取儲存在本機DAM中的資產，或瀏覽並使用遠端DAM中可用的資產。

Dynamic Media搭配OpenAPI功能提供數種其他好處，例如存取和使用內容片段中的遠端資產、擷取遠端資產的中繼資料等等。 進一步瞭解Dynamic Media的OpenAPI功能優於連線Assets](/help/assets/dynamic-media-open-apis-faqs.md)的其他[優點。

## 開始之前 {#pre-requisits-sites-integration}

* 為AEM as a Cloud Service設定下列[環境變數](/help/implementing/cloud-manager/environment-variables.md#add-variables)：

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX`參考程式識別碼<br>
     `eYYYY`參考環境識別碼

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]

  或在AEM Sites執行個體中為AEM 6.5設定[OSGi設定](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html)，請遵循下列步驟：

   1. 登入主控台並按一下&#x200B;**[!UICONTROL OSGi] >**或
使用直接URL；例如： `http://localhost:4502/system/console/configMgr`

   1. 新增&#x200B;**[!UICONTROL repositoryID]**= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot;和&#x200B;**[!UICONTROL imsClient]**= [IMSClientId]
深入瞭解[IMS驗證](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html)。

* 以IMS存取登入遠端DAM AEM as a Cloud Service例項。

* 在遠端DAM中開啟具有OpenAPI功能的Dynamic Media切換開關。

* 在AEM Sites例項中設定影像v3元件。 如果元件不存在，請下載並安裝[內容封裝](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0)。

## 從遠端DAM存取資產 {#fetch-assets}

Dynamic Media搭配OpenAPI功能，可讓您在本機AEM Sites頁面編輯器和AEM內容片段上存取遠端DAM例項中可用的資產。

![影像](/help/assets/assets/open-APIs.png)

### 在AEM頁面編輯器中存取遠端資產 {#access-assets-page-editor}

請依照下列步驟，在您的AEM Sites執行個體上使用AEM頁面編輯器中的遠端資產。 您可以在AEM as a Cloud Service和AEM 6.5中進行這項整合。

1. 移至&#x200B;**[!UICONTROL 網站]** > _您的網站_，其中有AEM **[!UICONTROL 頁面]**，您需要新增遠端資產。
1. 瀏覽至您打算新增遠端資產之網站中&#x200B;**[!UICONTROL 網站]**&#x200B;區段下的特定AEM **[!UICONTROL 頁面]**。
1. 選取頁面並按一下&#x200B;**[!UICONTROL 編輯(_e_)]**。 AEM **[!UICONTROL 頁面編輯器]**&#x200B;開啟。
1. 按一下「版面容器」並新增&#x200B;**[!UICONTROL Image]**&#x200B;元件。
1. 按一下&#x200B;**[!UICONTROL Image]**&#x200B;元件，然後按一下![設定圖示](/help/assets/assets/do-not-localize/settings-icon.svg)圖示。
1. 取消勾選&#x200B;**[!UICONTROL 從頁面]**&#x200B;繼承精選影像選項。
1. 按一下&#x200B;**[!UICONTROL 挑選]**&#x200B;並選取&#x200B;**[!UICONTROL 遠端]**。
   ![影像](/help/assets/assets/uncheck-inherit-option.jpg)

   系統會提示您登入。
1. 選取資產並按一下&#x200B;**[!UICONTROL 選取]**。
1. 新增替代文字並按一下&#x200B;**[!UICONTROL 完成]**。
   <br>遠端資產會出現在影像元件中。 您也可以在資產載入頁面時，或使用「預覽」索引標籤，驗證資產的傳送URL。 傳遞URL表示資產正由遠端存取。

您只能針對「影像核心元件v3」和「Teaser核心元件v2」 ，使用開箱即用的AEM頁面編輯器來存取遠端資產。 若為其他元件（包括自訂元件），需進行自訂，才能將Asset Selector與這些元件整合。

#### 影片：存取AEM頁面編輯器中的遠端資產

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### 存取AEM內容片段中的遠端資產 {#access-assets-content-fragment}

請依照下列步驟，在您的AEM Sites執行個體上使用AEM內容片段中的遠端資產。 您可以在AEM 6.5中執行這項整合，但無法在AEM as a Cloud Service上執行。

1. 移至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。
1. 選取出現內容片段的資產資料夾。
1. 選取內容片段並按一下&#x200B;**[!UICONTROL 編輯(_e_)]**。

   >[!NOTE]
   >
   >如果您沒有AEM內容片段模式，您可能需要[建立一個](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en)。

1. 按一下文字元件旁的![勾選圖示](/help/assets/assets/do-not-localize/checkmark-icon.svg)圖示。
1. 選取&#x200B;**[!UICONTROL 遠端]**&#x200B;以從遠端DAM擷取資產。 <br>
您可以視需要選擇**[!UICONTROL 本機]**&#x200B;或&#x200B;**[!UICONTROL 遠端]** DAM存放庫。

   ![影像](/help/assets/assets/cf-pick.jpg)
系統會提示您登入。
1. 選擇資產並按一下&#x200B;**[!UICONTROL 選取]**。
   <br>遠端資產URL會顯示在文字元件中。

#### 影片：存取AEM內容片段中的遠端資產

>[!VIDEO](https://video.tv.adobe.com/v/3427667)

### 在Edge Delivery Services中存取遠端資產 {#access-assets-eds}

您也可以存取Edge Delivery Services中的遠端資產。 如需詳細資訊，請參閱[使用透過Dynamic Media提供的Assets as a Cloud Service資產搭配OpenAPI功能](https://www.aem.live/docs/aem-assets-sidekick-plugin#utilizing-assets-from-assets-cloud-services-delivered-via-dynamic-media-with-openapi)。
