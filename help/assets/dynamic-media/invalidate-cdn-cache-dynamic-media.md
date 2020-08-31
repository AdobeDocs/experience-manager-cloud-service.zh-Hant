---
title: 透過動態媒體使CDN快取失效
description: 停用CDN（內容傳送網路）快取內容可讓您快速更新由動態媒體傳送的資產，而不需等待快取過期。
translation-type: tm+mt
source-git-commit: 30c7dddb52a6012d3c55cdb66ae0c9b1a3588fa3
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 1%

---


# 透過動態媒體使CDN快取失效 {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

動態媒體資產由CDN（內容傳送網路）快取，以便快速傳送給客戶。 不過，當您更新這些資產時，您可能會希望這些變更立即在您的網站上生效。 清除或停用CDN快取可讓您快速更新由動態媒體傳送的資產。 您不需等待快取使用TTL（存留時間）值（預設值為10小時）過期，而是可在動態媒體使用者介面內傳送要求，讓快取在數分鐘內過期。

>[!IMPORTANT]
>
>下列步驟僅適用於AEM上的Dynamic Media做為雲端服務。 此功能也要求您使用隨附於AEM Dynamic Media的現成可用CDN;不支援任何其他自訂CDN。 <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier to invalidate the CDN cache [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

另請參閱 [動態媒體中的快取概觀](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)。

**利用動態媒體使CDN快取失效**

*第1部分（共2部分）:建立CDN失效範本*

1. 在AEM中，以雲端服務的形式，點選「工 **[!UICONTROL 具>資產> CDN失效範本」。]**

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-template.png)

1. 在 **[!UICONTROL CDN失效範本頁面]** ，根據您的藍本執行下列其中一個選項：

   | 藍本 | 選項 |
   | --- | --- |
   | 我過去已使用Dynamic Media Classic建立CDN失效範本。 | 「建 **[!UICONTROL 立範本]** 」文字欄位會預先填入範本資料。 在這種情況下，您可以編輯範本，或繼續下一步驟。 |
   | 我需要建立範本。 我要輸入什麼？ | 在「建 **[!UICONTROL 立範本]** 」文字欄位中，輸入參照的影像URL（包括影像預設集或修飾元），而非下列範例中的特定影像ID: `<ID>`如果範本僅包含<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>`<ID>``https://<publishserver_name>/is/image/<company_name>/<ID>``<publishserver_name>` ，則動態媒體會填入，其中是Dynamic Media Classic中「一般設定」中定義之發佈伺服器名稱；the `<company_name>` is the name of your company root associated with this AEM instance, and `<ID>` is the selected assets through the asset picker to be unvalized.<br>任何預設集／修飾 `<ID>` 元貼文都會如同在URL定義中複製。<br>只有影像(即， `/is/image`可以根據範本自動形成)。<br>對於 `/is/content/`而言，使用資產選擇器新增資產（例如影片或PDF）並不會自動產生URL。 您必須改為在「CDN失效」範本中指定此類資產，或者您可以手動將URL新增至第2部分(共2 *部分)中的此類資產：設定CDN失效選項*。<br>**範例：**<br>&#x200B;在第一個範例中，失效範本與資 `<ID>` 產URL一起包含 `/is/content`。 For example, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. 動態媒體會根據此建立URL，而 `<ID>` 資產是透過您要失效的資產選擇器選取的資產。<br>在第二個範例中，失效範本包含Web屬性中使用之資產的完整URL, `/is/content` 並且不依賴資產選擇器。 例如，背 `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` 包是資產ID。<br>動態媒體支援的資產格式可失效。 CDN失效不支援的資 *產檔案類型* ，包括Postscript、Encapsulated Postscript、Adobe Illustrator、Adobe InDesign、Microsoft Powerpoint、Microsoft Excel、Microsoft Word和Rich Text格式。<br>建立範本時，請務必注意語法和錯字；動態媒體不會進行任何範本驗證。<br>請注意，您必須在此CDN失效範本或第2部分的「新增URL *****」文字欄位中，為影像智慧裁切指定URL:設定CDN失效選項。*<br>**重要：**CDN失效範本中的每個項目都必須位於其自己的行上。<br>*以下範本範例僅供圖例之用。* |

   ![CDN失效範本——建立](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. 在 **[!UICONTROL CDN失效範本頁面的右上角]** ，點選「 **[!UICONTROL 儲存]**」，然後點選「 **[!UICONTROL 確定」。]**<br>   *第2部分（共2部分）:設定CDN失效選項*
   <br>

1. 在AEM中，以雲端服務的形式，點選「工 **[!UICONTROL 具>資產> CDN失效」。]**

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. 在「 **[!UICONTROL CDN失效]** -新 **[!UICONTROL 增詳細資料]** 」頁面上，選取CDN失效的資產。

   ![CDN失效——新增詳細資料](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您決定保留「使CDN中與資產相關的 **[!UICONTROL Invalidate asset associated image presets in CDN]** 」（使資產相關的影像預設集失效）和「 *Invalidate based on template***** 」（基於範本失效）選項，則選定資產的基本URL會形成為失效。 您只應將此選項的排列方式用於影像。


   | 選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中與影像預設集相關聯的資產失效]** | （可選）勾選此選項時，選取的資產及其所有相關的影像預設集URL都會自動形成，以便快取失效。<br>資產及其相關的預先定義預設URL會自動形成為無效。 此選項僅適用於影像資產。 |
   | **[!UICONTROL 基於模板的失效]** | （可選）勾選此選項，僅使用已定義的URL建立範本。 |
   | **[!UICONTROL 新增資產]** | 使用「資產選擇器」來選擇您要廢止的資產。 您可以選取已發佈或未發佈的資產。<br>CDN的快取是以URL為基礎，而非以資產為基礎。 因此，您必須注意您網站上的完整URL。 在您決定這些URL後，您可以將它們新增至範本。 然後，您可以選取並新增這些資產，並在單一步驟中使URL無效。 <br>搭配使用此選項與CDN中的「使 **[!UICONTROL 資產相關的影像預設值無效]**」或「根 **[!UICONTROL 據範本失效]**」或兩者搭配使用。 |
   | **[!UICONTROL 新增 URL]** | 手動新增或貼上完整URL路徑至您要使其CDN快取失效的動態媒體資產。 如果您未在2的第1部分中建立CDN失效範本，請 ***使用此選項：建立CDN失效範本***，而且只有少數資產可供失效。<br>**重要：** 您新增的每個URL都必須位於其自己的行上。<br>您一次最多可以使1000個URL失效。 如果「新增URL」文字欄 **[!UICONTROL 位中的URL]** 數大於1000，則無法點選「下 **[!UICONTROL 一步」]**。 在這種情況下，您必須點選所選資產 **[!UICONTROL 右側的X]** ，或手動新增的URL，才能將其從失效清單中刪除。<br>請注意，您必須在CDN失效範本或此「新增URL」文字欄位中，為影像智慧裁切指 **[!UICONTROL 定URL]** 。 |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next.]**
1. 在「 **[!UICONTROL CDN失效]** - **[!UICONTROL Confirm]** 」（CDN確認）頁面上， **** URL清單方塊中會顯示您先前建立的CDN失效範本以及您剛新增的資產所產生的一或多個URL清單。

   例如，使用先前步驟中顯示的CDN失效範本範例，假設您新增了名為的單一資產 `spinset`。 當您點選「工 **[!UICONTROL 具>資產> CDN失效]** 」時，會在「 **[!UICONTROL CDN失效」中產生下列五個產生的URL - 「確認使用者介面]** 」:

   ![CDN失效——確認](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，點 **選URL右側的** X，將其從失效程式中刪除。

1. 在頁面的右上角，點選「 **[!UICONTROL Submit]** 」以開始CDN失效程式。

## 疑難排解CDN失效錯誤

在所有情況下，處理整個批以進行失效處理，或處理整個批失敗。

| 錯誤 | 說明 |
| --- | --- |
| *無法擷取所選資產的URL。* | 如果符合下列任一情形，則發生：<br>—— 找不到動態媒體設定。<br>-檢索通過讀取動態媒體配置的服務用戶時出現異常。<br>-動態媒體設定中遺失用來形成URL的發佈伺服器或公司根目錄。 |
| *有些URL未定義正確。 請更正並重新送出。* | 如果IPS CDN快取失效API傳回錯誤，指出URL轉介至其他公司，或URL無效，則發生IPS cdnCacheInvalidation API進行的驗證。 |
| *無法使CDN快取失效。* | 發生於CDN快取失效要求因任何其他原因而失敗時。 |
| *未輸入任何URL，因此無效。* | 發生於「 **[!UICONTROL CDN失效]** —— 確認」頁面中沒有URL，而您點選「提交」時 ******[!UICONTROL 發生。]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
