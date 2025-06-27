---
title: 從 [!DNL Admin View] 到 [!DNL Assets View]匯入中繼資料表單
description: 本文說明如何從 [!DNL Admin View] 匯入中繼資料表單至 [!DNL Assets View]
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 5fb4fe97-486a-4a91-af60-a7182efcc2f9
source-git-commit: fdd74e4d9b74600fd462e951046abfb1bb8e203b
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 8%

---

# 將中繼資料表單從[!DNL Admin View]匯入至[!DNL Assets View] {#import-metadata-forms-from-admin-view-to-assets-view}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 與 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 與 Edge Delivery Services 整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>使用者介面可擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用 Dynamic Media Prime 與 Ultimate</b></a>
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

[!DNL Adobe Experience Manager Assets]可讓您從[!DNL Admin View]將中繼資料表單及其資料夾關聯匯入至[!DNL Assets View]。

## 開始之前{#prerequisites-for-importing-metadata-forms-to-assets-view}

確保您具有管理員許可權，可將中繼資料表單及其資料夾關聯從[!DNL Admin View]匯入至[!DNL Assets View]。

## 將中繼資料表單匯入[!DNL Assets View]{#import-metadata-forms-to-assets-view}

以管理員身分，執行下列步驟，將[!DNL Admin View]中可用的中繼資料表單匯入至[!DNL Assets View]：

1. 導覽至[!DNL Assets View]首頁，然後按一下&#x200B;**[!UICONTROL 設定]**&#x200B;底下的&#x200B;**[!UICONTROL 中繼資料Forms]**&#x200B;以開啟&#x200B;**[!UICONTROL 中繼資料Forms]**&#x200B;頁面，其中顯示[!DNL Assets View]中可用的中繼資料表單清單。

   ![中繼資料表單頁面](/help/assets/assets/metadata-forms-page.png)

1. 選取&#x200B;**[!UICONTROL 匯入]**，會顯示處理訊息(例如，*正在處理2個中繼資料表單……請稍候。*)。 處理完成後，會顯示&#x200B;**[!UICONTROL 匯入中繼資料表單]**&#x200B;表格，其中包括[!DNL Admin View]中可用的中繼資料表單清單。 資料表列包含中繼資料表單名稱（**[!UICONTROL 名稱]**&#x200B;下）、與該表單關聯的資料夾（**[!UICONTROL 資料夾關聯]**&#x200B;下）以及在匯入表單之前預覽![預覽](/help/assets/assets/Preview.svg)表單的選項。

   ![匯入中繼資料Forms頁面](/help/assets/assets/import-metadata-forms-page.png)

   >[!NOTE]
   > 
   > 在&#x200B;**[!UICONTROL 匯入中繼資料Forms]**&#x200B;中，表格名稱旁的&#x200B;**[!UICONTROL 重複]**&#x200B;標籤顯示表單已套用至[!DNL Assets View]中的資料夾。 匯入該重複表單會覆寫套用至資料夾的現有表單。 若要避免此覆寫，請在匯入表單前重新命名表單。 按一下表單名稱以重新命名。

1. 按一下資料夾名稱旁的![選取資料夾](/help/assets/assets/x.svg) （在[!UICONTROL 資料夾關聯]下）以移除與表單的資料夾關聯。
1. 按一下![選取資料夾](/help/assets/assets/add-to-folder.svg)以選取資料夾，將對應的中繼資料表單指派給資料夾。
1. 按一下紅色圓圈可檢視不支援的中繼資料元件或表單中對應（這些元件或對應已從匯入中排除）的詳細資料。

   ![匯入中繼資料Forms頁面](/help/assets/assets/unsupported-import-elements.png)

1. 在資料表中選取一或多個表單，然後按一下&#x200B;**[!UICONTROL 開始匯入]**，將中繼資料表單及其相關資料夾匯入[!DNL Assets View]。 顯示處理訊息(例如，*正在匯入3個中繼資料表單。 請稍候！*)。 匯入完成後，成功訊息會確認表單已成功匯入，且&#x200B;**[!UICONTROL 中繼資料Forms]**&#x200B;頁面（共[!DNL Assets View]頁）會顯示最近匯入的表單以及[!DNL Assets View]中可用的現有表單。 您可以在此頁面上執行下列動作：

   * 按一下資料行標題，依[!UICONTROL 名稱]、[!UICONTROL 修改時間]或[!UICONTROL 作者]將資料表排序。
   * 選取匯入的表單並按一下&#x200B;**[!UICONTROL 從資料夾移除]**，然後驗證資料夾路徑中的資料夾名稱，以確認資料夾已正確移轉。
     ![驗證中繼資料表單頁面](/help/assets/assets/confirm-ported-folder.png)
   * 選取匯入的表單，然後按一下&#x200B;**[!UICONTROL 編輯]**&#x200B;以檢視中繼資料表單的所有支援設定。 請參閱[設定中繼資料Forms](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/metadata#metadata-forms)，以取得有關中繼資料表單、其元件和欄位的詳細資訊。

   ![驗證中繼資料表單頁面](/help/assets/assets/verify-metadata-forms-page.png)

## 驗證匯入的中繼資料表單{#Verify-the-imported-metadata-forms}

將中繼資料表單從[!DNL Admin View]匯入至[!DNL Assets View]後，請依照下列步驟驗證匯入：

1. 導覽至匯入的中繼資料表單的任何相關資料夾。
1. 導覽至[資產的詳細資料頁面](/help/assets/navigate-assets-view.md#preview-assets)，並確認支援的中繼資料元件、元件欄位和欄位值已從[!DNL Admin View]同步。 請參閱Assets Essentials](https://experienceleague.adobe.com/en/docs/experience-manager-assets-essentials/help/metadata)文章中的[中繼資料，以取得有關中繼資料元件、元件欄位和欄位值的詳細資訊。

   >[!NOTE]
   >
   > 在[[!DNL Assets View] 詳細資料頁面](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/metadata-assets-view#metadata-forms)或[[!DNL Admin View] 屬性頁面](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/administer/metadata-schemas)中，中繼資料屬性值的變更會在兩個介面之間自動同步。 但是，表單中的結構變更（例如新增或移除欄位或其他修改）不會同步。
