---
title: 將遠端 AEM Assets 與 AEM Sites 整合
description: 瞭解如何使用核准的AEM Assets來設定及連結AEM網站。
exl-id: 382e6166-3ad9-4d8f-be5c-55a7694508fa
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 2%

---

# 將遠端 AEM Assets 與 AEM Sites 整合  {#integrate-approved-assets}

有效管理數位資產對於跨各種線上平台提供吸引人且一致的品牌體驗至關重要。 Dynamic Media具備OpenAPI功能，可啟用AEM Sites與AEM Assets as a Cloud Service之間的緊密整合，進而增強數位資產管理。 這項創新功能可讓您輕鬆在多個AEM環境中共用和管理不同型別的已核准數位資產，精簡網站作者和內容編輯的工作流程。

具備OpenAPI功能的Dynamic Media可讓Sites作者直接在AEM頁面編輯器和[內容片段](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html)中使用遠端DAM的資產，進而簡化內容建立和管理程式。

使用者可以將多個AEM Sites執行個體（對最大數量沒有任何限制）連線到遠端DAM部署，這是優於[連線的Assets](use-assets-across-connected-assets-instances.md)功能的顯著優點。

![影像](/help/assets/assets/connected-assets-rdam.png)

初始設定後，使用者可以在AEM Sites執行個體上建立頁面，並視需要新增資產。 新增資產時，他們可以選取儲存在本機DAM中的資產，或瀏覽並使用遠端DAM中可用的資產。

具備OpenAPI功能的Dynamic Media提供數種其他優點，例如存取和使用內容片段中的遠端資產、擷取遠端資產的中繼資料等等。 進一步瞭解Dynamic Media （具有OpenAPI功能）優於Connected Assets[&#128279;](/help/assets/dynamic-media-open-apis-faqs.md)的其他優點。

## 開始之前 {#pre-requisites-sites-integration}

若要支援使用Dynamic Media搭配OpenAPI功能的遠端資產，需要：

* AEM 6.5 SP 18+或AEM as a Cloud Service

* 核心元件2.23.2版或更新版本

* 為AEM as a Cloud Service設定下列[環境變數](/help/implementing/cloud-manager/environment-variables.md#add-variables)：

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxxx-eyyyyy.adobeaemcloud.com&quot; <br>

     `pXXXX`參考程式識別碼<br>
     `eYYYY`參考環境識別碼

  這些變數是使用AEM as a Cloud Service環境的Cloud Manager使用者介面設定的，會作為您的本機Sites例項。

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]：您必須提交Adobe支援票證才能取得IMS使用者端ID。

     或在AEM Sites執行個體中為AEM 6.5設定[OSGi設定](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html)，請遵循下列步驟：

   1. 登入主控台並按一下&#x200B;**[!UICONTROL OSGi] >**&#x200B;或
使用直接URL；例如： `https://localhost:4502/system/console/configMgr`

   1. 依照以下方式設定&#x200B;**新一代動態媒體設定** (`NextGenDynamicMediaConfigImpl`) OSGi設定，將值取代為您遠端資產環境的值。

      ```text
        imsClient="<ims-client-ID>"
        enabled=B"true"
        imsOrg="<ims-org>@AdobeOrg"
        repositoryId="<repo-id>.adobeaemcloud.com"
      ```

      `imsOrg`不是強制輸入。
      `repositoryId` = &quot;delivery-pxxxxx-eyyyyyy.adobeaemcloud.com&quot;
其中`pXXXX`參考了方案ID
      `eYYYY`參考環境識別碼

      ![新一代動態媒體設定OSGi設定視窗](/help/assets/assets/remote-assets-osgi.png)

  深入瞭解[IMS驗證](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html)。

  如需如何設定OSGi的詳細資訊，請參閱下列檔案：

   * [為AEM as a Cloud Service設定Adobe Experience Manager as a Cloud Service的OSGi](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html)
   * [為AEM 6.5設定OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html)

* 以IMS存取登入遠端DAM AEM as a Cloud Service例項。 這指對遠端DAM環境具有IMS存取許可權的Sites作者。

* 在AEM Sites例項中設定影像v3元件。 如果元件不存在，請下載並安裝[內容封裝](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0)。

## 設定 HTTPS {#https}

通常建議使用HTTP來執行您的所有生產AEM執行個體。 不過，您的本機開發環境可能不會依此設定。 不過，使用Dynamic Media搭配OpenAPI的遠端資產需要HTTPS才能運作。

[使用本指南](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html)設定HTTPS，無論您想使用遠端資產，包括開發環境。

## 從遠端DAM存取資產 {#fetch-assets}

具OpenAPI功能的Dynamic Media可讓您在本機AEM Sites頁面編輯器和AEM內容片段上，存取遠端DAM執行個體中可用的資產。

![影像](/help/assets/assets/open-APIs.png)

### 在AEM頁面編輯器中存取遠端資產 {#access-assets-page-editor}

請依照下列步驟，在您的AEM Sites執行個體上使用AEM頁面編輯器中的遠端資產。 您可以在AEM as a Cloud Service和AEM 6.5中進行這項整合。

1. 移至&#x200B;**[!UICONTROL 網站]** > _您的網站_，其中有AEM **[!UICONTROL 頁面]**，您需要新增遠端資產。
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

您只能針對「影像核心元件v3」和「Teaser核心元件v2」存取內建AEM頁面編輯器中的遠端資產。 若為其他元件（包括自訂元件），需進行自訂，才能將Asset Selector與這些元件整合。

#### 影片：存取AEM頁面編輯器中的遠端資產

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### 存取AEM內容片段中的遠端資產 {#access-assets-content-fragment}

請依照下列步驟，在您的AEM Sites執行個體上使用AEM內容片段中的遠端資產。 您可以在AEM 6.5中執行這項整合，但無法在AEM as a Cloud Service中執行。

1. 移至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]**。
1. 選取出現內容片段的資產資料夾。
1. 選取內容片段並按一下&#x200B;**[!UICONTROL 編輯(_e_)]**。

   >[!NOTE]
   >
   >如果您沒有AEM內容片段模式，您可能需要[建立一個](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en)。

1. 按一下文字元件旁的![勾選圖示](/help/assets/assets/do-not-localize/checkmark-icon.svg)圖示。
1. 選取&#x200B;**[!UICONTROL 遠端]**&#x200B;以從遠端DAM擷取資產。 <br>
您可以視需要選擇&#x200B;**[!UICONTROL 本機]**&#x200B;或&#x200B;**[!UICONTROL 遠端]** DAM存放庫。

   ![影像](/help/assets/assets/cf-pick.jpg)
系統會提示您登入。
1. 選擇資產並按一下&#x200B;**[!UICONTROL 選取]**。
   <br>遠端資產URL會顯示在文字元件中。

#### 影片：存取AEM內容片段中的遠端資產

>[!VIDEO](https://video.tv.adobe.com/v/3427667)

### 在Edge Delivery Services中存取遠端資產 {#access-assets-eds}

在Microsoft Word、Google Docs或Universal Editor中編寫內容時，您可以存取遠端資產，然後將內容發佈至Edge Delivery Services。 您也可以搭配OpenAPI使用Dynamic Media來提供品牌核准的資產，並利用其提供的許多其他優點。 如需詳細資訊，請參閱[在編寫AEM Assets的內容時整合Edge Delivery Services](/help/assets/integrate-aem-assets-edge-delivery-services.md)。
