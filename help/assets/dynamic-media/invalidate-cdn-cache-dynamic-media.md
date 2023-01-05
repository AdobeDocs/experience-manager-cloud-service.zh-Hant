---
title: 透過Dynamic Media使內容傳送網路快取失效
description: 了解如何使您的CDN（內容傳遞網路）快取內容失效，讓您快速更新Dynamic Media所傳送的資產，而不必等待快取過期。
feature: Asset Management
role: Admin,User
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: db0451e76564f238b34555aafa3692202887a1d6
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 1%

---

# 透過 Dynamic Media 使 CDN 快取失效 {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Dynamic Media資產會由CDN（內容傳遞網路）快取，以快速傳遞給客戶。 不過，當您更新這些資產時，您希望這些變更立即在您的網站上生效。 清除或使CDN快取失效，可讓您快速更新由Dynamic Media傳送的資產。 您不再需要等待快取使用TTL（存留時間）值（預設為10小時）到期。 反之，您可以從Dynamic Media使用者介面傳送要求，讓快取在數分鐘內過期。

>[!NOTE]
>
>您必須使用Adobe Experience Manager Dynamic Media隨附的Adobe套件CDN，才能使用此功能。 此功能不支援任何其他自訂CDN。

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

如果您已啟用 [智慧型影像](/help/assets/dynamic-media/imaging-faq.md) 在您的帳戶中，當您使用Adobe套件的CDN時，可以清除單一基礎URL，以清除具有不同查詢字串的所有URL。

例如，使用 `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`，也會讓下列URL失效：

* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?wid=300`
* `https://weekendsite.scene7.com/is/image/<CUSTOMER-NAME>/image?$PLP$`
* 等等。

不過，不支援智慧型影像處理的一般網域並非如此，例如 `s7d1.scene7.com`. 此類網域仍需要完整的URL才能成功失效。

**若要透過Dynamic Media使CDN快取失效：**

*第1部分，共2部分：建立CDN失效範本*

1. 在Adobe Experience Manager as a Cloud Service中，前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL CDN失效範本]**.

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-template.png)

1. 在 **[!UICONTROL CDN失效範本]** 頁面，根據您的案例執行下列其中一個選項：

   | 藍本 | 選項 |
   | --- | --- |
   | 我過去已使用Dynamic Media Classic建立CDN失效範本。 | 此 **[!UICONTROL 建立範本]** 文字欄位已預先填入您的範本資料。 在這種情況下，您可以編輯範本，或繼續下一個步驟。 |
   | 我必須建立一個模板。 我要輸入什麼？ | 在 **[!UICONTROL 建立範本]** 文字欄位，輸入影像URL（包括影像預設集或修飾元）以參考 `<ID>`，而非下列範例中的特定影像ID:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果範本僅包含 `<ID>`，則Dynamic Media填入 `https://<publishserver_name>/is/image/<company_name>/<ID>` where `<publishserver_name>` 是在Dynamic Media Classic的「一般設定」中定義的發佈伺服器名稱。 此 `<company_name>` 是與此Experience Manager例項相關聯的公司根名稱，且 `<ID>` 是透過資產選擇器選取的資產，即會失效。<br>之後的任何預設集/修飾元 `<ID>` 會在URL定義中照原樣複製。<br>只有影像， `/is/image` — 可根據範本自動形成。<br>針對 `/is/content/`，使用資產選擇器新增視訊或PDF等資產不會自動產生URL。 您必須改為在「CDN失效」範本中指定此類資產，或者您可以在 *第2部分（共2部分）:設定CDN失效選項*.<br>**範例：**<br>&#x200B;在第一個範例中，失效範本包含 `<ID>` 以及具有 `/is/content`. 例如， `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media會根據此路徑，透過 `<ID>` 是透過您要失效的資產選擇器選取的資產。<br>在第二個範例中，失效範本包含Web屬性中使用之資產的完整URL，搭配 `/is/content` （不依賴資產選擇器）。 例如， `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` 背包是資產ID。<br>Dynamic Media支援的資產格式可失效。 資產檔案類型為 *not* 支援的CDN失效包括PostScript®、封裝的PostScript®、Adobe Illustrator、Adobe InDesign、Microsoft® Powerpoint、Microsoft® Excel、Microsoft® Word和RTF格式。<br><br>·建立範本時，請務必注意語法和錯字；Dynamic Media不進行任何範本驗證。<br>· CDN失效範本最多可儲存2500個字元的文字。<br>·在此CDN失效範本或 **[!UICONTROL 新增URL]** 文字欄位 *第2部分：設定CDN失效選項。*<br>· CDN失效範本中的每個項目必須位於其自己的行上。<br>·下列CDN失效範本範例僅供示範之用。 |

   ![CDN失效範本 — 建立](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >CDN失效範本最多可儲存2500個字元的文字。

1. 位於 **[!UICONTROL CDN失效範本]** 頁面，選取 **[!UICONTROL 儲存]**，然後選取 **[!UICONTROL 確定]**.<br>

   *第2部分（共2部分）:設定CDN失效選項*
   <br>

1. 在Experience Manageras a Cloud Service中，前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL CDN失效]**.

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. 在 **[!UICONTROL CDN失效]** - **[!UICONTROL 添加詳細資訊]** 頁面中，選取CDN失效的資產。

   ![CDN失效 — 新增詳細資料](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果您決定保留選項 **[!UICONTROL 使CDN中與資產相關聯的影像預設集無效]** *和* **[!UICONTROL 根據模板無效]** 取消勾選，則選取資產的基礎URL會形成為無效。 僅對影像使用此選項排列。


   | 選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中與影像預設集相關聯的資產失效]** | （選用）勾選此選項時，系統會自動形成選取的資產及其所有相關的影像預設集URL，以利快取失效。<br>資產及其相關聯的預先定義預設URL會自動形成為無效。 此選項僅適用於影像資產。 |
   | **[!UICONTROL 根據範本失效]** | （選用）核取此選項，僅使用已定義的範本來形成URL。 |
   | **[!UICONTROL 新增資產]** | 使用「資產選擇器」來選取您要使其無效的資產。 您可以選取已發佈或未發佈的資產。<br>CDN的快取是以URL為基礎，而非以資產為基礎。 因此，您必須注意您網站上的完整URL。 在您決定這些URL後，即可將它們新增至範本。 接著，您可以選取並新增這些資產，並在單一步驟中使URL無效。 <br>將此選項與 **[!UICONTROL 使CDN中與資產相關聯的影像預設集無效]**，或 **[!UICONTROL 根據範本失效]**，或兩者皆有。 |
   | **[!UICONTROL 新增 URL]** | 手動新增或貼上完整的URL路徑至您要使其CDN快取失效的Dynamic Media資產。 如果您未在 ***第1部分，共2部分：建立CDN失效範本***，且只有數個資產可讓其失效。<br>**重要：** 您新增的每個URL都必須位於各自的行上。<br>您一次最多可使1000個URL無效。 若 **[!UICONTROL 新增URL]** 文本欄位大於1000，您無法選擇 **[!UICONTROL 下一個]**. 在這種情況下，您必須選取 **[!UICONTROL X]** 或手動新增的URL，以從失效清單中刪除該資產的右側。<br>在CDN失效範本或此範本中，指定影像智慧裁切的URL **[!UICONTROL 新增URL]** 文字欄位。 |

1. 在頁面的右上角附近，選取 **[!UICONTROL 下一個]**.
1. 在 **[!UICONTROL CDN失效]** - **[!UICONTROL 確認]** 頁面，在 **[!UICONTROL URL]** 清單方塊中，您會看到一或多個URL的清單，這些URL是從您先前建立的CDN失效範本以及您剛新增的資產中產生。

   例如，使用先前步驟中顯示的CDN失效範本範例，假設您新增了名為 `spinset`. 當您前往 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL CDN失效]**，會在 **[!UICONTROL CDN失效 — 確認]** 使用者介面：

   ![CDN失效 — 確認](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，請選取 **X** 的URL右側，將其從失效程式中刪除。

1. 在頁面的右上角附近，選取 **[!UICONTROL 提交]** 開始CDN失效程式。

## 疑難排解CDN失效錯誤

在所有情況下，會處理整個批次以失效，或處理整個批次失敗。

| 錯誤 | 解釋 |
| --- | --- |
| *無法擷取所選資產的URL。* | 在符合下列任一情況時發生：<br> — 找不到Dynamic Media設定。<br> — 擷取可透過讀取Dynamic Media設定的服務使用者時發生例外狀況。<br>-Dynamic Media設定中缺少發佈伺服器或用來形成URL的公司根。 |
| *有些URL未正確定義。 更正並重新提交。* | 如果IPS CDN快取失效API傳回錯誤，則會發生此情況。 此錯誤表示URL參照不同的公司，或該URL無效，如IPS cdnCacheInvalidation API所完成的驗證。 |
| *無法使CDN快取失效。* | 當CDN快取失效請求因任何其他原因而失敗時發生。 |
| *輸入的URL無效。* | 若 **[!UICONTROL CDN失效]** - **[!UICONTROL 確認]** 頁面，然後選取 **[!UICONTROL 提交]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
