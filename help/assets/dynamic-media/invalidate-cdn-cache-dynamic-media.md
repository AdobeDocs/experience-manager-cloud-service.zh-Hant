---
title: 通過Dynamic Media使內容傳遞網路快取無效
description: 瞭解如何使您的CDN（內容分發網路）快取內容失效，以便您快速更新由Dynamic Media分發的資產，而不是等待快取過期。
feature: Asset Management
role: Admin,User
exl-id: c631079b-8082-4ff7-a122-dac1b20d8acd
source-git-commit: 5c8e3a7ea87b70707b2613ffc7b4f51341303614
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 1%

---

# 通過Dynamic Media使CDN快取無效 {#invalidating-cdn-cache-for-dm-assets-in-aem-cs}

Dynamic Media資產由CDN（內容交付網路）快取，以便快速交付給您的客戶。 但是，當您更新這些資產時，您希望這些更改在您的網站上立即生效。 清除或使CDN快取失效允許您快速更新由Dynamic Media傳送的資產。 您不必再使用TTL（生存時間）值（預設值為十小時）等待快取過期。 相反，您可以從Dynamic Media用戶介面發送請求，使快取在幾分鐘內過期。

>[!NOTE]
>
>此功能要求您使用Adobe Experience ManagerDynamic Media附帶的Adobe捆綁CDN。 此功能不支援任何其他自定義CDN。

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

如果已啟用 [智慧映像](/help/assets/dynamic-media/imaging-faq.md) 在您的帳戶上，並且您正在使用Adobe捆綁的CDN，您可以通過清除單個基本URL來清除具有不同查詢字串的所有URL。

例如，無效 `https://weekendsite.scene7.com/is/image/grundfos/image`，也使以下URL無效：

* `https://weekendsite.scene7.com/is/image/grundfos/image`
* `https://weekendsite.scene7.com/is/image/grundfos/image?wid=300`
* `https://weekendsite.scene7.com/is/image/grundfos/image?$PLP$`
* 等等。

但是，對於不支援智慧映像的通用域，如 `s7d1.scene7.com`。 這樣的域仍需要完整的URL才能成功地進行無效工作。

**要通過Dynamic Media使CDN快取失效：**

*第1部分（共2部分）:建立CDN無效模板*

1. 在Adobe Experience Manager as a Cloud Service，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL CDN無效模板]**。

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-template.png)

1. 在 **[!UICONTROL CDN無效模板]** 頁，根據您的方案執行以下選項之一：

   | 方案 | 選項 |
   | --- | --- |
   | 我過去已經使用Dynamic Media Classic建立了CDN無效模板。 | 的 **[!UICONTROL 建立模板]** 文本欄位將預先填充模板資料。 在這種情況下，您可以編輯模板，也可以繼續執行下一步。 |
   | 我得建立一個模板。 我輸入什麼？ | 在 **[!UICONTROL 建立模板]** 文本欄位，輸入引用的影像URL（包括影像預設或修飾符） `<ID>`，而不是像以下示例中所示的特定影像ID:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>如果模板僅包含 `<ID>`然後Dynamic Media填滿 `https://<publishserver_name>/is/image/<company_name>/<ID>` 何處 `<publishserver_name>` 是在Dynamic Media Classic的「常規設定」中定義的發佈伺服器的名稱。 的 `<company_name>` 是與此Experience Manager實例關聯的公司根的名稱， `<ID>` 是通過資產選取器要失效的選定資產。<br>後面的任何預設/修飾符 `<ID>` 在URL定義中按原樣複製。<br>只有影像， `/is/image` — 可以基於模板自動形成。<br>對於 `/is/content/`，使用資產選取器添加視頻或PDF等資產不會自動生成URL。 相反，您必須在CDN無效模板中指定此類資產，或者可以在中手動將URL添加到此類資產 *第2部分（共2部分）:設定CDN無效選項*。<br>**示例：**<br>&#x200B;在第一個示例中，失效模板包含 `<ID>` 以及資產URL `/is/content`。 比如說， `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`。 Dynamic Media基於此路徑形成URL, `<ID>` 是通過要失效的資產選取器選擇的資產。<br>在第二個示例中，失效模板包含Web屬性中使用的資產的完整URL, `/is/content` （不依賴於資產選取器）。 比如說， `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` 背包是資產ID。<br>在Dynamic Media支援的資產格式有資格失效。 資產檔案類型 *不* 支援CDN失效，包括PostScript®、封裝PostScript®、Adobe Illustrator、Adobe InDesign、Microsoft® Powerpoint、Microsoft® Excel、Microsoft® Word和富文本格式。<br><br>·建立模板時，請務必注意語法和拼寫；Dynamic Media不執行任何模板驗證。<br>· CDN無效模板可保存最多2500個字元的文本。<br>·在此CDN無效模板或 **[!UICONTROL 添加URL]** 文本欄位 *第二部分：正在設定CDN無效選項。*<br>· CDN失效模板中的每個條目必須位於其自己的行上。<br>·以下CDN失效模板示例僅供演示。 |

   ![CDN無效模板 — 建立](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >CDN失效模板可以保存最多2500個字元的文本。

1. 在右上角 **[!UICONTROL CDN無效模板]** ，選擇 **[!UICONTROL 保存]**，然後選擇 **[!UICONTROL 確定]**。<br>

   *第2部分（共2部分）:設定CDN無效選項*
   <br>

1. 在Experience Manageras a Cloud Service中，轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL CDN無效]**。

   ![CDN驗證功能](/help/assets/assets-dm/cdn-invalidation-path.png)

1. 在 **[!UICONTROL CDN無效]** - **[!UICONTROL 添加詳細資訊]** 頁面，選擇CDN失效的資產。

   ![CDN無效 — 添加詳細資訊](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >如果你決定保留 **[!UICONTROL 使CDN中與資產關聯的影像預設無效]** *和* **[!UICONTROL 基於模板無效]** 未選中，則選定資產的基URL被形成為無效。 僅對影像使用此選項排列。


   | 選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 使 CDN 中與影像預設集相關聯的資產失效]** | （可選）選中此選項時，所選資產及其所有關聯的影像預設URL都會自動形成，以用於快取無效。<br>自動形成資產及其相關聯的預定義預設URL以進行無效。 此選項僅適用於映像資產。 |
   | **[!UICONTROL 基於模板的無效]** | （可選）選中此選項可僅使用URL形成的已定義模板。 |
   | **[!UICONTROL 新增資產]** | 使用資產選取器選擇要失效的資產。 您可以選擇已發佈或未發佈的資產。<br>CDN上的快取是基於URL的，而不是基於資產的。 因此，您必須瞭解您網站上的完整URL。 確定這些URL後，可將其添加到模板。 然後，您可以選擇和添加這些資產，並使URL在一步中失效。 <br>將此選項與 **[!UICONTROL 使CDN中與資產關聯的影像預設無效]**&#x200B;或 **[!UICONTROL 基於模板的無效]**，或兩者兼有。 |
   | **[!UICONTROL 新增 URL]** | 手動向要使其CDN快取失效的Dynamic Media資產添加或貼上完整URL路徑。 如果未在中建立CDN無效模板，則使用此選項 ***第1部分（共2部分）:建立CDN無效模板***，並且只有少數資產需要失效。<br>**重要提示：** 您添加的每個URL必須位於其自己的行上。<br>您可以在指定時間使最多1000個URL無效。 如果 **[!UICONTROL 添加URL]** 文本欄位大於1000，無法選擇 **[!UICONTROL 下一個]**。 在這種情況下，必須選擇 **[!UICONTROL X]** 的子菜單。<br>在CDN無效模板或此模板中為智慧映像作物指定URL **[!UICONTROL 添加URL]** 的子菜單。 |

1. 在頁面右上角附近，選擇 **[!UICONTROL 下一個]**。
1. 在 **[!UICONTROL CDN無效]** - **[!UICONTROL 確認]** 的 **[!UICONTROL URL]** 清單框中，您將看到從先前建立的CDN無效模板以及剛剛添加的資產中生成的一個或多個URL的清單。

   例如，使用前面步驟中顯示的CDN無效模板示例，假設您添加了名為 `spinset`。 當您轉到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL CDN無效]**，它將在 **[!UICONTROL CDN無效 — 確認]** 用戶介面：

   ![CDN無效 — 確認](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   如有必要，請選擇 **X** 的子菜單。

1. 在頁面右上角附近，選擇 **[!UICONTROL 提交]** 開始CDN無效過程。

## 排除CDN失效錯誤

在所有情況下，要麼處理整個批以失效，要麼處理整個批失敗。

| 錯誤 | 解釋 |
| --- | --- |
| *無法檢索所選資產的URL。* | 如果滿足以下任何情形，則發生：<br> — 找不到Dynamic Media配置。<br> — 檢索讀取Dynamic Media配置的服務用戶時出現異常。<br> — 在Dynamic Media配置中缺少用於形成URL的發佈伺服器或公司根。 |
| *某些URL定義不正確。 更正並重新提交。* | 如果IPS CDN快取無效API返回錯誤，則發生。 錯誤表示URL引用了其他公司，或URL無效，因為IPS cdnCacheInvalidation API已完成驗證。 |
| *無法使CDN快取無效。* | 如果CDN快取失效請求因任何其他原因失敗，則發生。 |
| *未輸入要失效的URL。* | 如果中沒有URL **[!UICONTROL CDN無效]** - **[!UICONTROL 確認]** ，然後選擇 **[!UICONTROL 提交]**。 |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
