---
title: 在您的AEM Sites頁面中使用資產之前，請先預覽資產
description: 具OpenAPI功能的Dynamic Media可讓您在Adobe Experience Manager (AEM) Sites預覽頁面上預覽資產。 此資產預覽可讓您和您的利害關係人在發佈作者頁面（包含更新的資產）以供公眾使用之前，檢閱及驗證資產的更新。
role: Admin, User
source-git-commit: e343cc5754ec5565e57a5a932d59d7bfe78c6027
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---


# 在您的AEM Sites頁面中使用資產之前，請先預覽資產 {#asset-preview-using-Dynamic-Media-with-OpenAPI-capabilities}

[!DNL Dynamic Media with OpenAPI capabilities]可讓您在公開使用資產之前，先預覽[!DNL Adobe Experience Manager (AEM) Sites]作者頁面中可用的資產。 資產預覽可在您網站的作者和預覽層級上使用。

若要[在AEM Sites預覽頁面上預覽資產](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities)，請新增您要預覽的資產或取代即時網站頁面中現有的資產，以更新網站的作者頁面。 然後，將更新的作者頁面發佈到預覽層級以產生預覽URL。

與利害關係人共用預覽頁面，以收集對更新資產的視覺品質和內容一致的意見回饋。 根據意見調整資產。 在稽核週期中建立並管理資產的多個版本。

完成供公眾使用的資產後，請在製作頁面中更新資產，並將頁面發佈至發佈層級以供公眾存取。

## 開始之前{#prerequisites-for-previewing-assets-using-Dynamic-Media-with-OpenAPI-capabilities}

確定您擁有：

* 存取[!DNL AEM Assets as a Cloud Service]。
* 編輯資產的Status屬性的許可權。
* [已將[!UICONTROL 預覽]值新增至套用至包含要預覽之資產的資料夾的中繼資料表單的[!UICONTROL 基本]索引標籤[!UICONTROL 中可用的]狀態](/help/assets/metadata-assets-view.md#edit-metadata-forms)中繼資料屬性。
  ![新增預覽選項](/help/assets/assets/metedata-form-preview.png)
* 產生預覽權杖的金鑰。 [聯絡Adobe支援](https://helpx.adobe.com/in/contact.html)並提出金鑰要求。

## 在網站預覽頁面中預覽資產 {#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities}

您可以預覽已核准的新資產或資產。 核准的資產只會顯示在您的已上線Sites頁面上。

執行以下步驟，將資產狀態設定為在[!DNL Assets View]中預覽，然後將您的Sites編寫頁面發佈到預覽層級，以產生頁面的預覽URL：

1. 執行下列步驟，將資產狀態設定為&#x200B;**[!UICONTROL 預覽]**：

   1. 在[!DNL Assets View]中，選取&#x200B;**[!UICONTROL Assets]**&#x200B;並導覽至您的資料夾。
   1. 選取要預覽的資產。
   1. 按一下&#x200B;**[!UICONTROL 詳細資料]**。
   1. 在[!UICONTROL 資訊面板]中，將&#x200B;**[!UICONTROL 狀態]**&#x200B;設定為&#x200B;**[!UICONTROL 預覽]**，然後按一下&#x200B;**[!UICONTROL 儲存]**。
      ![預覽](/help/assets/assets/preview-boat-at-bay.png)

1. 導覽至您的「網站」撰寫頁面。 執行[存取AEM頁面編輯器中的遠端資產](/help/assets/integrate-remote-approved-assets-with-sites.md#access-remote-assets-in-aem-page-editor)區段中的步驟，以使用「資產選擇器」面板選取您最近設定為預覽（狀態）的資產。

   >[!NOTE]
   >
   > 「資產選擇器」會顯示最近狀態更新設為「已核准」或「預覽」的資產。

1. 使用&#x200B;**[!UICONTROL 管理出版物]**&#x200B;選項將您的頁面發佈到預覽層。 執行[將內容發佈到預覽](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/previewing-content)區段中的步驟，將您的頁面發佈到預覽層。 發佈後，產生頁面的預覽URL。 「預覽」頁面會顯示Sites頁面中的資產（具有最近的狀態更新）。

與利害關係人共用此預覽URL，以進行檢閱和獲得回饋。 確保您的利害關係人有權存取預覽頁面。 請參閱[存取預覽服務](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments#access-preview-service)，以取得關於提供預覽頁面存取權的資訊。

>[!NOTE]
>
>根據預設，[影像V3核心元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/wcm-components/image#version-and-compatibility)支援預覽版本的資產。 當您使用[Asset Selector](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/asset-selector-upload)面板選取資產的預覽版本（具有預覽狀態的資產）時，影像V3元件會自動在預覽層級（在您的Sites作者頁面上的預覽版本）中轉譯。

完成資產版本後，[將您的頁面發佈到發佈階層](#publish-your-pages-to-publish-tier)以供公眾使用。

## 使用核准的資產發佈您的頁面以供公眾使用{#publish-your-pages-to-publish-tier}

最終確定供公眾使用的資產版本後，將資產狀態設定為&#x200B;**[!UICONTROL 已核准]**。 然後將您的頁面發佈至發佈階層。 執行以下步驟以發佈您的頁面：

1. 請依照上文[預覽網站預覽頁面](#asset-preview-on-sites-pages-using-Dynamic-Media-with-OpenAPI-capabilities)區段中的步驟1，將資產狀態變更為&#x200B;**[!UICONTROL 已核准]**。
1. 導覽至您的Sites作者頁面，並將其發佈至[!DNL Publish tier]。 從頁面編輯器[區段執行](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/sites/authoring/page-editor/publishing#publishing-from-the-page-editor)發佈中的步驟，以發佈頁面。
或者，請依照[從網站主控台](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/sites/authoring/sites-console/publishing-pages#publishing-from-the-sites-console)區段發佈頁面的步驟操作，從網站主控台發佈您的頁面。

   >[!NOTE]
   >
   > 發佈層級上只能傳遞已核准的資產。 先核准資產，然後再將頁面發佈到發佈層級以供公眾使用。

   ![頁面已發佈](/help/assets/assets/the-page-has-been-publushed.png)
確認訊息&#x200B;**[!UICONTROL 頁面已發佈]**，在成功發佈後顯示。 導覽至發佈層級上的已發佈頁面，確認更新已上線且內容如預期顯示。

