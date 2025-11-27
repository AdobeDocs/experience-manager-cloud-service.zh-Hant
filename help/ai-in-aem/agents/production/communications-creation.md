---
title: 溝通建立技能
description: 瞭解Experience Production Agent的通訊建立技能，以及如何使用自然語言建立互動式通訊。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 01fce6fcdf1c8ada0422a84fccb9a89f395e2a0e
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---


# 溝通建立技能 {#ic-creation-skill}

>[!NOTE]
>
> 「通訊建立」技能目前為Alpha版。 如果您想要參與，請將您的正式電子郵件地址傳送至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)。

互動式通訊是個人化的資料導向檔案，專為商業通訊而設計，例如帳戶對帳單、原則檔案、帳單、歡迎套件和福利通知。 不同於從使用者收集輸入的表單，互動式通訊會產生具有動態、收件者特定內容的輸出檔案。

通訊建立技能是Experience Production Agent的一項功能，旨在使用自然語言提示開發互動式通訊。 此技能會自動產生個人化、資料導向的列印對應(PDF格式)。 技能是透過AI Assistant浮出水面的。

建立溝通技巧的一些主要優點包括：

* **加速通訊開發**：使用簡單的自然語言命令快速建立通訊，不需要學習傳統產品介面。
* **一致且符合品牌的信件**：使用核准的範本和樣式，建立符合您組織品牌、範本和樣式指引的通訊。
* **較低的技術障礙**：可讓商務使用者輕鬆建立通訊，而不需要進階的技術或深厚的產品專業知識。

## 功能 {#capabilities}

<!-- * **Create personalized communications with plain text prompt**: You can create communication documents for print (in PDF format) by submitting your requirements in plain language. The agent automatically generates appropriate document structures, layouts, and data bindings based on your natural language description. -->

* **從範本建立**：您可以使用核准的組織範本，以確保品牌一致性和法規遵循標準。 代理程式會運用您現有的範本和風格指南，建立符合法規要求的品牌對應。

* **將現有的影像和檔案匯入並轉換成互動式通訊**：您可以將現有的檔案匯入並轉換成互動式通訊。 代理程式會分析上傳的內容以偵測欄位、保留版面，並建立與動態內容功能之間的資料導向對應。 支援的格式包括PDF、影像(JPG、PNG)和手繪範本。


## 範例提示 {#sample-prompts}

* *使用位於https://[aem-author-url]/path/to/pdf/file*&#x200B;的範本，為貸款宣告建立通訊
* *在https://[aem-author-url]/path/to/pdf/file*&#x200B;從PDF建立通訊
* *從位於https://[aem-author-url]/path/to/image/file*&#x200B;的影像檔建立通訊
* 使用PDF檔案建立信件，網址為https://[aem-author-url]/path/to/pdf/file


## 精簡您的通訊內容 {#refine-with-ic-editor}


使用AI助理建立初始通訊結構後，您可以使用互動式通訊編輯器來調整及增強您的檔案。 在互動式通訊編輯器中，您可以使用自然語言提供提示以：

* **新增欄位和內容**：使用自然語言提示新增欄位、文字區塊、影像、圖表、表格和其他元件至您的通訊檔案。 代理程式會解譯您的指示，並以適當的結構和格式插入適當的元素。

* **編輯欄位和內容**：透過對話式命令修改通訊檔案中的現有欄位和內容。 更新欄位屬性、變更文字內容、調整資料繫結，以及調整元件設定。

* **移除欄位和內容**：使用自然語言指示，從通訊檔案中刪除不要的欄位、元件或區段。 代理程式會移除指定的元素，同時維持檔案結構和版面配置完整性。

* **樣式欄位和內容**：透過自然語言提示將格式設定和樣式套用至欄位和內容。 調整字型、顏色、對齊方式、間距和其他視覺屬性，以符合您的品牌方針和設計需求。

### 精簡通訊的提示範例 {#sample-prompts-refining}

* *產生車輛保險索賠結算函*
* *將免責宣告文字變為斜體*
* *將免責宣告文字的字型大小變更為12*
* *將免責宣告文字的字型顏色更新為紅色*
* *將頁首與頁尾文字方塊的背景顏色更新為淺灰色*
* *新增包含簽名和確認欄位的新免責宣告面板*
* *移除確認文字欄位*
* *新增包含三欄的付款詳細資料表*
* *更新原則編號欄位與中心*&#x200B;的對齊方式
* *將條款與條件區段的行距變更為1.5*

如需互動式通訊編輯器功能的詳細資訊，請參閱[互動式通訊檔案](/help/forms/introduction-to-interactive-communication.md)。

## 啟用 {#activation}

若要為貴組織啟用Experience Production Agent，必須透過Adobe啟動啟用。 透過以下方式聯絡以開始此程式：

* 電子郵件： `experience-production-agent@adobe.com`
* 或者，請聯絡您指定的Adobe客戶團隊。

聯絡時，請務必提供您的AEM as a Cloud Service組織ID。

