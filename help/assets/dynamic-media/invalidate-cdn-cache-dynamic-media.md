---
title: 透過Dynamic Media使內容傳遞網路快取失效
description: 瞭解如何使CDN （內容傳遞網路）快取內容失效，以讓您快速更新Dynamic Media傳送的資產，而不是等待快取過期。
contentOwner: Rick Brough
feature: Asset Management
role: Admin,User
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 2%

---

# 透過 Dynamic Media 使 CDN 快取失效 {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

CDN （內容遞送網路）會快取Dynamic Media資產，以快速遞送給您的客戶。 不過，當您更新這些資產時，希望這些變更立即在您的網站上生效。 清除或使CDN快取失效，可讓您快速更新Dynamic Media傳送的資產。 您不必再等待快取使用TTL （存留時間）值（預設為10小時）過期。 反之，您可以從Dynamic Media使用者介面傳送請求，讓快取在數分鐘內過期。

>[!NOTE]
>
>此功能需要您使用Adobe Experience Manager Dynamic Media隨附的Adobe隨附CDN。 此功能不支援任何其他自訂CDN。

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

如果您已啟用 [智慧型影像](/help/assets/dynamic-media/imaging-faq.md) 若您的帳戶使用Adobe隨附的CDN，您可清除單一基底URL，以清除所有包含不同查詢字串的URL。

例如，失效 `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`，也會讓下列URL失效：

* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?wid=300`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?$PLP$`
* 以此類推.

然而，不支援智慧型影像的一般網域則不是這種情況，例如 `s7d1.scene7.com`. 這類網域仍需要完整URL才能成功讓失效工作。

**透過Dynamic Media使CDN快取失效：**

*第1部分（共2部分）：建立CDN失效範本*

1. 在Adobe Experience Manager as a Cloud Service中，前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL CDN失效範本]**.

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-template.png)

1. 於 **[!UICONTROL CDN失效範本]** 頁面，根據您的情境執行下列其中一個選項：

   | 情境 | 選項 |
   | --- | --- |
   | 我過去曾使用Dynamic Media Classic建立CDN失效範本。 | 此 **[!UICONTROL 建立範本]** 文字欄位已預先填入您的範本資料。 在這種情況下，您可以編輯範本或繼續下一步驟。 |
   | 我必須建立範本。 我輸入什麼？ | 在 **[!UICONTROL 建立範本]** 文字欄位，輸入參考的影像URL （包括影像預設集或修飾元） `<ID>`，而非如下列範例所示的特定影像ID：<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果範本僅包含 `<ID>`，然後Dynamic Media填入 `https://<publishserver_name>/is/image/<company_name>/<ID>` 位置 `<publishserver_name>` 是在Dynamic Media Classic的「一般設定」中定義的發佈伺服器名稱。 此 `<company_name>` 是與此Experience Manager執行個體相關聯的公司根目錄名稱，以及 `<ID>` 是透過要失效的資產選擇器選取的資產。<br>以下的任何預設集/修飾元 `<ID>` 會依原樣複製URL定義。<br>只有影像，也就是 `/is/image` — 可根據範本自動形成。<br>對象 `/is/content/`，使用資產選擇器新增視訊或PDF等資產不會自動產生URL。 反之，您必須在CDN失效範本中指定這類資產，或者您可以手動將URL新增到中的這類資產 *第2部分（共2部分）：設定CDN失效選項*.<br>**範例：**<br>&#x200B;在第一個範例中，失效範本包含 `<ID>` 連同資產URL，具有 `/is/content`. 例如， `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media會根據此路徑來表單URL，使用 `<ID>` 是要讓透過資產選擇器選取的資產失效。<br>在第二個範例中，失效範本包含您的Web屬性中使用的資產的完整URL，並具有 `/is/content` （不取決於資產選擇器）。 例如， `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` 其中揹包是資產ID。<br>Dynamic Media支援的資產格式符合失效的條件。 符合以下條件的資產檔案型別 *not* CDN失效支援的功能包括PostScript®、封裝PostScript®、Adobe Illustrator、Adobe InDesign、Microsoft®Powerpoint、Microsoft®Excel、Microsoft®Word和RTF格式。<br><br>·建立範本時，請務必留意語法和拼字錯誤；Dynamic Media不會進行任何範本驗證。<br>· CDN失效範本最多可儲存2500個字元的文字。<br>·在此CDN失效範本中或在 **[!UICONTROL 新增URL]** 中的文字欄位 *第2部分：設定CDN失效選項。*<br>· CDN失效範本中的每個專案都必須位於其自己的行上。<br>·下列CDN失效範本範例僅供示範之用。 |

   ![CDN失效範本 — 建立](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >CDN失效範本最多可儲存2500個字元的文字。

1. 在的右上角 **[!UICONTROL CDN失效範本]** 頁面，選取 **[!UICONTROL 儲存]**，然後選取 **[!UICONTROL 確定]**.<br>

   *第2部分（共2部分）：設定CDN失效選項*
   <br>

1. 在Experience Manageras a Cloud Service中，前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL CDN失效]**.

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. 於 **[!UICONTROL CDN失效]** - **[!UICONTROL 新增詳細資料]** 頁面中，選取CDN失效的資產。

   ![CDN失效 — 新增詳細資料](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您決定保留選項 **[!UICONTROL 使CDN中與影像預設集相關聯的資產失效]** *和* **[!UICONTROL 根據範本失效]** 取消勾選，則會形成所選資產的基礎URL以進行失效。 僅對影像使用此選項排列。


   | 選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中與影像預設集相關聯的資產失效]** | （選用）勾選此選項時，系統會自動形成所選資產及其所有相關影像預設集URL，讓快取失效。<br>資產及其相關之預先定義的預設URL會自動形成以失效。 此選項僅適用於影像資產。 |
   | **[!UICONTROL 根據範本失效]** | （選用）核取此選項以僅使用已定義的範本來形成URL。 |
   | **[!UICONTROL 新增資產]** | 使用資產選取器來選取您要失效的資產。 您可以選取已發佈或已取消發佈的資產。<br>CDN上的快取是以URL為基礎，而非以資產為基礎。 因此，您必須注意您網站上的完整URL。 在您決定這些URL後，可以將其新增至範本。 然後，您可以選取並新增這些資產，並在一個步驟中使URL失效。 <br>使用此選項搭配 **[!UICONTROL 使CDN中與影像預設集相關聯的資產失效]**，或 **[!UICONTROL 根據範本失效]**，或兩者。 |
   | **[!UICONTROL 新增 URL]** | 手動將完整URL路徑新增或貼上至您想要讓CDN快取失效的Dynamic Media資產。 如果您未在中建立CDN失效範本，請使用此選項 ***第1部分（共2部分）：建立CDN失效範本***，且只有少數資產會失效。<br>**重要：** 您新增的每個URL都必須位於其自己的行中。<br>您一次最多可以使1000個URL失效。 如果 **[!UICONTROL 新增URL]** 文字欄位大於1000，您無法選取 **[!UICONTROL 下一個]**. 在這種情況下，您必須選取 **[!UICONTROL X]** 右側所選資產或手動新增URL的，可從失效清單中刪除該資產。<br>在CDN失效範本中或以下範本中指定影像智慧裁切的URL **[!UICONTROL 新增URL]** 文字欄位。 |

1. 在頁面的右上角附近，選取 **[!UICONTROL 下一個]**.
1. 於 **[!UICONTROL CDN失效]** - **[!UICONTROL 確認]** 頁面，在 **[!UICONTROL URL]** 清單方塊中，您會看到一或多個從您先前建立的CDN失效範本以及您剛才新增的資產所產生的URL清單。

   例如，使用先前步驟中顯示的CDN失效範本範例，假設您新增了名為的單一資產 `spinset`. 當您前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL CDN失效]**，則會在中產生下列5個URL **[!UICONTROL CDN失效 — 確認]** 使用者介面：

   ![CDN失效 — 確認](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，請選取 **X** URL右側，用於從失效程式中刪除它。

1. 在頁面的右上角附近，選取 **[!UICONTROL 提交]** 以開始CDN失效程式。

## 疑難排解CDN失效錯誤

在所有情況下，系統都會處理整個批次以使其失效，或是整個批次都失敗。

| 錯誤 | 解釋 |
| --- | --- |
| *無法擷取所選資產的URL。* | 在符合下列任一情況時發生：<br> — 找不到Dynamic Media設定。<br> — 擷取讀取Dynamic Media設定的服務使用者時發生例外狀況。<br>- Dynamic Media設定中缺少用於形成URL的發佈伺服器或公司根目錄。 |
| *部分URL未正確定義。 更正並重新提交。* | 在IPS CDN快取失效API傳回錯誤時發生。 根據IPS cdnCacheInvalidation API所做的驗證，此錯誤會指出URL參照了不同的公司或URL無效。 |
| *無法使CDN快取失效。* | 在CDN快取失效要求因任何其他原因而失敗時發生。 |
| *沒有輸入要失效的URL。* | 如果沒有URL存在於 **[!UICONTROL CDN失效]** - **[!UICONTROL 確認]** 頁面，然後選取 **[!UICONTROL 提交]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
