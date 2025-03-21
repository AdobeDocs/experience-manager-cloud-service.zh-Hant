---
title: Dynamic Media中的報告
description: 瞭解如何為Dynamic Media傳送失敗的URL請求錯誤報告。
contentOwner: Rick Brough
feature: Asset Management
role: User
hide: true
hidefromtoc: true
exl-id: 2488f813-df15-4dbb-8747-f827ee5925e1
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 6%

---

# 請求失敗的Dynamic Media傳送URL的錯誤報告

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets與Edge Delivery Services整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

您可以要求錯誤報告，識別傳送時失敗的Dynamic Media URL。 此報表是最多五天的資料彙總，並以CSV格式提供。 錯誤報告包含下列資訊：

* 失敗的Dynamic Media傳送URL — 失敗的URL是Dynamic Media產生的URL，無法在傳送時產生任何內容。
* 反向連結URL — 呼叫失敗傳遞URL的來源反向連結URL。
* 失敗計數 — 載入傳遞URL而導致失敗的次數。

當您請求錯誤報告時，Adobe Dynamic Media團隊會以CSV格式將報告透過電子郵件傳送給您。 涵蓋從提出要求之日起的五天期間。

您可以每月為指定公司要求一次錯誤報告。

**為失敗的Dynamic Media傳遞URL要求錯誤報告：**

1. [傳送電子郵件至reports-dynamic-media@adobe.com](mailto:reports-dynamic-media@adobe.com)，其中包含與您的Dynamic Media帳戶相關聯的公司名稱。

   如果您不知道公司名稱，請參閱&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL 動態媒體設定]**&#x200B;中的[動態媒體設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html?lang=zh-Hant#configuring-dynamic-media-cloud-services)頁面。 在[Dynamic Media設定瀏覽器]頁面上，按一下&#x200B;**[!UICONTROL global]**，選取&#x200B;*[Dynamic_Media_folder_icon]*&#x200B;核取方塊，然後選取&#x200B;**[!UICONTROL 編輯]**。 您必須在AEM中擁有管理員許可權，才能存取Dynamic Media設定頁面。

   ![存取Dynamic Media設定頁面。](/help/assets/dynamic-media/assets/reporting-accessdmconfig.png)
