---
title: 使用Adobe Express在Content Hub中編輯影像
description: 使用Adobe Express在Content Hub中編輯影像
exl-id: c9777862-226c-4d39-87da-9c4a30437dc5
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 18%

---

# 在Content Hub中編輯影像 {#edit-images-content-hub}

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

![使用Adobe Express在Content Hub中編輯影像](assets/edit-images-content-hub.png)

>[!AVAILABILITY]
>
>現已提供 PDF 格式的 Content Hub 指南。下載完整指南，並使用 Adobe Acrobat AI 助理來回答您的查詢問題。
>
>[!BADGE Content Hub 指南 PDF]{type=Informative url="https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub可讓您使用Adobe Express建立新內容。 您可以使用易於使用的工具來編輯現有內容、使用範本和品牌元素製作品牌變化版本，並使用 Adobe Firefly 的最新 GenAI 功能來建立新內容。

## 先決條件 {#prereqs-edit-image-content-hub}

有權存取Adobe Express和有權將資產重新混合到新變化的[Content Hub使用者](/help/assets/deploy-content-hub.md#onboard-content-hub-users-remix-assets)可以使用Content Hub編輯影像。

>[!NOTE]
>
您可以使用[!DNL Adobe Express]編輯PNG和JPG/JPEG檔案型別的影像。

## 使用 [!DNL Adobe Express] 編輯影像 {#edit-images-using-content-hub}

若要使用Content Hub編輯影像：

1. 按一下您需要編輯之影像的資產卡上可用的&#x200B;**[!DNL Open in Adobe Express]**。 或者，按一下影像以開啟其詳細資料，然後按一下[!DNL Adobe Express]標誌。 接著會載入適用於Adobe Express的內嵌編輯器，而不會離開Content Hub。

   您可以利用[!DNL Adobe Express]功能來執行所有與影像編輯相關的動作，例如[調整影像大小](https://helpx.adobe.com/express/using/resize-image.html)、[移除或變更背景顏色](https://helpx.adobe.com/express/using/remove-background.html)、[裁切影像](https://helpx.adobe.com/express/using/crop-image.html)、將影像與AI產生的影像或文字結合，等等。

1. 執行修改並按一下&#x200B;**[!UICONTROL 儲存]**，將編輯後的資產儲存為下列任一格式型別：

   * **[!UICONTROL PNG]** （作為高品質影像格式使用）
   * **[!UICONTROL JPG]** （適用於小型檔案）
   * **[!UICONTROL PDF]** （適用於檔案）

   ![使用 Adobe Express 儲存影像](assets/adobe-express-save-as.png)

1. 在&#x200B;**[!UICONTROL 另存新檔]**&#x200B;欄位中指定資產名稱。

1. 使用&#x200B;**[!UICONTROL 促銷活動名稱]**&#x200B;欄位指定資產的促銷活動名稱。 您可以使用現有的名稱或建立新名稱。 輸入名稱時，Content Hub會提供您更多選項。<!--You can define multiple Campaign names for your upload. While you are typing a name, either click anywhere else within the dialog box or press the `,` (Comma) key to register the name.-->

   作為最佳作法，Adobe建議您在其餘欄位中指定值，並為您上傳的資產建立增強的搜尋體驗。

1. [選擇性]定義&#x200B;**[!UICONTROL 關鍵字]**、**[!UICONTROL 管道]**、**[!UICONTROL 時間範圍]**&#x200B;和&#x200B;**[!UICONTROL 地區]**&#x200B;欄位的值。 依關鍵字、管道和位置來標籤和分組資產，可讓使用您核准公司內容的每個人都能找到這些資產並保持其井然有序。

1. 按一下&#x200B;**[!UICONTROL 另存為新資產]**&#x200B;以儲存資產。

管理員也可以設定將資產新增至Content Hub時顯示的必填和選用欄位，例如行銷活動名稱、關鍵字、管道等。 如需詳細資訊，請參閱[設定Content Hub使用者介面](configure-content-hub-ui-options.md#configure-upload-options-content-hub)。
