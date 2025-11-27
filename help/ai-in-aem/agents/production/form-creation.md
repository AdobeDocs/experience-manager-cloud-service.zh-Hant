---
title: 表單建立技能
description: 瞭解Experience Production代理程式的表單建立技能，以及如何使用自然語言從頭開始建立表單。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 01fce6fcdf1c8ada0422a84fccb9a89f395e2a0e
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---


# 表單建立技能 {#form-creation-skill}

表單建立技能是Experience Production Agent的一項功能，旨在使用自然語言提示開發表單。 此技能會自動產生適當的表單結構和欄位型別。 技能是透過AI Assistant浮出水面的。

表單建立技能的一些主要優點包括：

* **加速表單開發**：使用快速建立表單
簡單的自然語言命令，無需學習傳統的產品介面。
* **一致的品牌體驗**：使用核准的範本和樣式，建立符合您組織品牌、範本和樣式指導方針的表單。
* **較低的技術障礙**：可讓商務使用者輕鬆建立表格，而不需要進階的技術或深厚的產品專業知識。

## 功能 {#capabilitiess}

* **建立具有純文字提示的新表單**：您可以透過以純文字提交您的要求來建立表單。 代理程式會根據您的自然語言說明和指定的範本，自動產生適當的表單結構、欄位型別和品牌上體驗。 此功能可加速表單建立，同時確保維持品牌和合規性標準。

* **匯入PDF檔案並將其轉換為表單**：您可以將現有的PDF檔案匯入並轉換為表單。 代理程式會分析已上傳的內容，以偵測欄位型別、保留版面，並透過回應式設計和驗證邏輯來增強表單，同時確保維護品牌和合規性標準。

  使用任何上述功能時，系統會提示您選擇要建立的表單型別、指定核心元件式最適化表單範本或Edge Delivery Services式最適化表單範本，並指示您儲存表單的偏好路徑。 如果您是根據Edge Delivery Services建立表單，也可以指定存放庫的GitHub URL。


### 範例提示 {#sample-prompts}

* *建立包含名稱、電子郵件和訊息欄位的意見回饋收集表單*
* *建立具有產品評等（1-5顆星）、評論欄位和選擇性電子郵件的客戶意見表單*
* *建立包含名稱、電子郵件、主旨下拉式清單和訊息欄位的連絡人表單*
* *建立包含個人資訊、帳戶偏好設定和條款接受的登錄檔單*
* *匯入PDF檔案(位於&#39;https://[aem-author-url]/path/to/pdf/file*)，以建立信用卡申請表
* *使用&#39;<https://github.com/wkndforms/wesecure>&#39;*&#x200B;的樣版建立意見反應表單

## 精簡您的表單 {#refine-with-forms-experience-builder}

使用AI Assistant建立初始表單結構後，您可以使用Forms Experience Builder來：

* **更新表單**：透過視覺化編輯器新增或修改欄位、調整欄位型別，以及視需要更新樣式。

* **更新版面配置**：重新排列區段、群組或欄位，調整間距，並修改視覺階層，以提升使用性，並確保您的表單對您的對象清晰且直覺。

* **新增商業邏輯**：建立條件式邏輯、顯示/隱藏規則、欄位相依性，以及定義驗證規則。

* **設定提交**：設定提交表單資料的位置，包括設定電子郵件通知、與工作流程的整合，或與外部系統的連線。

如需詳細資訊，請參閱[Forms Experience Builder檔案](/help/forms/experience-builder/product-overview.md)。


## 啟用 {#activation}

若要為貴組織啟用Experience Production Agent，必須透過Adobe啟動啟用。 透過以下方式聯絡以開始此程式：

* 電子郵件： `experience-production-agent@adobe.com`
* 或者，請聯絡您指定的Adobe客戶團隊。

聯絡時，請務必提供您的AEM as a Cloud Service組織ID。


<!-- 
#### Import and convert {#import-and-convert}

Transform existing documents into interactive digital forms. The agent analyzes uploaded content to detect field types, preserve layouts, and enhance forms with responsive design and validation logic. Supported formats include Acroforms, XFA PDFs, flat PDFs, images (JPG, PNG), and hand-drawn form photographs.

>[!VIDEO](https://video.tv.adobe.com/v/3474042)

**Prompt examples:**

* *Convert the attached PDF file to an adaptive form*
* *Transform this scanned form image into an interactive digital form*
* *Import the employee onboarding PDF and create an editable form*
* *Convert this paper form photograph into a digital form with validation*
-->

<!-- 
### Embed an existing form to a sites page {#embed-existing-form}

The form creation skill enables seamless integration of existing forms into any sites page through natural language commands. Rather than manually locating, copying, and embedding form components, users can simply specify which form to add and where to place it. The agent handles the technical implementation, ensuring proper rendering and functionality.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Embed the contact form to the homepage*
* *Add the existing customer feedback form to the support page*
* *Insert the newsletter signup form into the footer section*
* *Place the registration form on /content/site/signup*
* *Add form "contact-us-2024" to the current page*
-->

<!-- 
### Build and add a form to an existing sites page {#build-and-add-form}

The form creation skill combines form creation and site integration in a single conversational workflow. Users can describe the form they need and specify where to add it, and the agent creates the form and embeds it into the specified page automatically. This eliminates the traditional multi-step process of creating a form separately and then manually adding it to a page.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Create a newsletter signup form with email field and add it to the footer*
* *Build a quick contact form with name, email, and message, then add it to /content/about-us*
* *Add a feedback form with rating stars and comment field to this page*
* *Create a simple survey form with 5 questions and embed it on the customer portal homepage*
* *Build an event registration form with name, email, and date selection, then add it to /content/events/conference-2025*
-->
