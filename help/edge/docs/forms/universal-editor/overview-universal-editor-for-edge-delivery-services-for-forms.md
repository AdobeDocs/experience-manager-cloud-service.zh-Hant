---
title: Edge Delivery Services for Forms 的通用編輯器
description: 使用 Edge Delivery Services for Forms 的通用編輯器建立自適應表單。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: d711e0d1-a2fc-4aa6-af87-6e77a7bc5d2e
source-git-commit: 9ef4c5638c2275052ce69406f54dda3ea188b0ef
workflow-type: ht
source-wordcount: '1012'
ht-degree: 100%

---


# Edge Delivery Services for Forms 的通用編輯器

<span class="preview">這是一項預先發佈功能，可透過我們的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">預先發佈管道</a>取得。</span>

通用編輯器提供簡單、視覺化且直覺易用的所見即所得 (WYSIWYG) 介面，徹底改變 Adobe Edge Delivery Services 建立表單的方式。這是專為內容創作者和表單製作者而設計，消除傳統表單建置流程的複雜性，讓非技術使用者也可以存取使用。

使用通用編輯器，您可以使用預先建立的元件 (如文字欄位、核取方塊和選項按鈕) 快速設計回應式、互動式表單。其強大的功能集支援動態規則、無縫資料整合和進階的個人化功能，確保每種表單都符合您的需求。

無論您是管理客戶端的輕量轉譯、確保跨瀏覽器相容性，或者遵守嚴格的無障礙標準，通用編輯器皆是建立和管理表單的精簡型解決方案。

![通用編輯器](/help/edge/docs/forms/universal-editor/assets/universal-editor.png){width=80%, align-center}

## Edge Delivery Services for Forms 通用編輯器的主要功能



| ![WYSIWYG 介面](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg) | ![規則編輯器](/help/edge/docs/forms/universal-editor/assets/rule-editor.svg) | ![提交動作](/help/edge/docs/forms/universal-editor/assets/submit-actions.svg) |
|:-------------:|:-------------:|:-------------:|
| [**WYSIWYG 介面**](/help/edge/docs/forms/universal-editor/universal-editor-user-interface.md) | [**規則編輯器**](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) | [**提交動作**](/help/edge/docs/forms/universal-editor/submit-action.md) |
| 通用編輯器是提供表單設計功能的 WYSIWYG 介面，具有預先建立的元件資料庫、回應式設計、使用範本建立表單和即時欄位修改。 | 規則編輯器讓使用者能夠透過事件驅動的規則、即時驗證，以及利用輕量級 JavaScript 和 JSON 進行錯誤處理來建立動態表單互動。 | 提交動作支援後端整合、條件式提交邏輯、安全端點和預處理器，能簡化提交工作流程。 |

| ![發佈/取消發佈](/help/edge/docs/forms/universal-editor/assets/publish-unpublish.svg) | ![回應式模式](/help/edge/docs/forms/universal-editor/assets/responsive.svg) | ![自訂元件](/help/edge/docs/forms/universal-editor/assets/custom-components.svg) |
|:-------------:|:-------------:|:-------------:|
| [**發佈/取消發佈**](/help/edge/docs/forms/universal-editor/publish-forms.md) | [**回應式模式**](/help/edge/docs/forms/universal-editor/responsive-layout.md) | [**自訂元件**](/help/edge/docs/forms/universal-editor/create-custom-component.md) |
| 輕鬆掌控表單的可見度，只需點按幾下即可直接從編輯器發佈或取消發佈表單。 | 設計可跨裝置 (桌上型電腦、平板電腦和行動裝置) 順暢適應的表單。使用回應式模式預覽和測試各種螢幕尺寸的表單。 | 開發人員可以利用自訂元件為特定組織使用案例量身打造獨特的元素，藉此擴展表單功能。 |

| ![樣式](/help/edge/docs/forms/universal-editor/assets/personalization.svg) | ![預填服務](/help/edge/docs/forms/universal-editor/assets/prefill-services.svg) | ![A/B 測試](/help/edge/docs/forms/universal-editor/assets/experimentation-ab-testing.svg) |
|:-------------:|:-------------:|:-------------:|
| [**樣式**](/help/edge/docs/forms/universal-editor/style-theme-forms.md) | **預填服務** (即將推出) | [**A/B 測試**](https://github.com/adobe/aem-experimentation/blob/main/documentation/experiments.md) |
| 使用 CSS 設定樣式讓開發人員能夠自訂表單元素的外觀，並建立與網站美學相符且具視覺吸引力的設計。 | 預填服務會自動使用多個來源的相關使用者資料填寫表單欄位，減少手動輸入並增強使用者體驗。 | A/B 測試讓組織能夠針對不同的表單設計、版面和功能進行實驗，以便找到效能最好的變體。 |

| ![分析與追蹤](/help/edge/docs/forms/universal-editor/assets/analyticsandtracking.svg) | ![表單片段](/help/edge/docs/forms/universal-editor/assets/form-fragments.svg) | ![資料繫結](/help/edge/docs/forms/universal-editor/assets/data-binding.svg) |
|:-------------:|:-------------:|:-------------:|
| [**分析與追蹤**](https://www.aem.live/developer/martech-integration) | **表單片段** (即將推出) | [**資料繫結**](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md) |
| 透過內建的分析與追蹤功能，深入了解使用者行為、表單互動和提交率，利用資料來達成表單最佳化。 | 表單片段可以實現重複使用，只要建立一個常用區段，便能在多個表單中重複使用，確保一致性並減少維護工作量。 | 利用資料繫結功能，可以將表單欄位與後端資料來源直接連線，支援即時更新和進階資料對應。 |

| ![驗證碼](/help/edge/docs/forms/universal-editor/assets/captcha.svg) | ![嵌入表單](/help/edge/docs/forms/universal-editor/assets/embedding-forms.svg) | ![感謝設定](/help/edge/docs/forms/universal-editor/assets/thank-you.svg) |
|:-------------:|:-------------:|:-------------:|
| [**驗證碼**](/help/edge/docs/forms/universal-editor/recaptcha-forms.md) | **嵌入表單** (即將推出) | [**感謝設定**](/help/edge/docs/forms/universal-editor/submit-action.md#show-a-custom-thank-you-message-on-adaptive-form-submission-submit-action-message-ue) |
| 使用 reCAPTCHA 保護表單避免遭受自動機器人攻擊，確保資料彙集安全且可靠。 | 使用通用編輯器的內建嵌入元件，將表單直接嵌入至 Edge Delivery Services Sites 頁面中。 | 輕鬆自訂在成功提交表單後，欲呈現給使用者看的確認訊息或頁面。 |


<!-- ![Universal Editor](/help/edge/docs/forms/universal-editor/assets/generate-forms.svg)  **WYSIWYG interface for Form creation**: Universal Editor provides a WYSIWYG interface for form design. It provides pre-built component library, responsive design support, and template-based form creation. You can instantly add or remove form fields and modify field properties (like label, data binding, validation). You can also plugin custom form components to Universal Editor.


* **Rule editor**: The rule editor stands out as a powerful mechanism for creating sophisticated form interactions. It supports event-driven rules, instant validation, and error handling through lightweight JavaScript and JSON-based definitions. This allows developers to implement complex form logic, such as conditional field visibility, automatic calculations, and dynamic form behaviour without extensive coding.

* **Submit actions**: Submit Actions enable form submission workflows. These actions provide comprehensive backend integration options, supporting protocols like REST API. The system allows you configure data pre-processors for automatic data transformation, conditional submission logic based on form field values, and secure endpoint connections. Organizations can define complex submission rules that validate data, and manage form responses with granular control.

* **Pre-fill services:** Pre-fill Services enhance user experience by intelligently populating form fields with relevant data. These services connect to various data sources, including user profiles, browser local storage, and external databases. The mechanism supports dynamic data population, enabling automatic completion of form fields based on contextual information. Users benefit from reduced manual data entry, while administrators gain flexibility in configuring pre-fill rules across different form types and scenarios. The pre-fill functionality adapts to different authentication methods, including session-based approaches and token-based systems, ensuring both convenience and security.

* **Data binding capabilities**: Data binding in the Universal Editor enables direct, dynamic connections between form fields and backend data sources. This feature allows real-time synchronization of form data, supporting complex data mapping scenarios. The system supports transforming form inputs into structured database records with minimal configuration. Advanced mapping supports nested data structures, allowing complex form designs to interact seamlessly with intricate data models.

* **Internationalization/localization capabilities**: Internationalization support ensures global accessibility, with multi-language rendering, right-to-left language compatibility, and locale-specific formatting.

* **Analytics and tracking mechanisms**: The built-in analytics and tracking mechanisms provide comprehensive insights into form interactions, submission rates, and user behavior, enabling continuous optimization of form design and performance. 

* **Experimentation (A/B Testing)**: The Universal Editor supports experimentation by allowing organizations to run A/B tests on form designs to identify the best-performing layouts or features.

* **Task Management via Adobe Workfront**: Integration with Adobe Workfront allows teams to manage tasks related to form creation and maintenance, ensuring streamlined collaboration and efficient workflows.

* **Editor Customization via UI Extension**: Developers can extend the functionality of the Universal Editor through UI extensions, enabling tailored solutions that fit specific organizational needs. -->

## 預先建立的表單元件

通用編輯器提供以下立即可用的表單元件：

<table>
  <thead>
    <tr>
      <th></th> 
      <th>表單元件</th>
      <th>說明</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="22"><img src="/help/edge/docs/forms/universal-editor/assets/adaptive-forms-components.png" alt="表單元件" style="width: 100%;"></td> 
      <td><b>折疊面板</b></td>
      <td>用於將內容進行組織的可收摺面板結構。</td>
    </tr>
    <tr>
      <td><b>按鈕</b></td>
      <td>替導覽或自訂邏輯等動作新增互動式元素。</td>
    </tr>
    <tr>
      <td><b>驗證碼</b></td>
      <td>要求使用者透過 Google reCaptcha 或 HCaptcha 完成人工驗證任務，以避免垃圾郵件。</td>
    </tr>
    <tr>
      <td><b>核取方塊</b></td>
      <td>讓使用者能夠設定核取方塊。</td>
    </tr>
    <tr>
      <td><b>核取方塊群組</b></td>
      <td>讓使用者能夠從一個群組中選取多個選項。</td>
    </tr>
    <tr>
      <td><b>日期挑選器</b></td>
      <td>讓使用者能夠利用行事曆介面選取日期。</td>
    </tr>
    <tr>
      <td><b>下拉式清單</b></td>
      <td>提供預定義清單中的單選或多選選項。</td>
    </tr>
    <tr>
      <td><b>電子郵件</b></td>
      <td>透過基本格式驗證擷取電子郵件地址。</td>
    </tr>
    <tr>
      <td><b>檔案附件</b></td>
      <td>允許上傳文件、影像或其他類型的檔案。</td>
    </tr>
    <tr>
      <td><b>表單片段</b></td>
      <td>地址欄位或聯絡方式等區段的可重複使用表單元件。</td>
    </tr>
    <tr>
      <td><b>影像</b></td>
      <td>支援在表單中上傳和顯示影像。</td>
    </tr>
    <tr>
      <td><b>模型</b></td>
      <td>呈現快顯視窗對話框，通常用於警報、附加資訊或確認。</td>
    </tr>
    <tr>
      <td><b>數值欄位</b></td>
      <td>擷取數值輸入，允許驗證數字或範圍。</td>
    </tr>
    <tr>
      <td><b>面板</b></td>
      <td>使用可展開/可收摺面板將表單區段進行組織。</td>
    </tr>
    <tr>
      <td><b>選項按鈕</b></td>
      <td>允許從一個群組的選項中進行單項選取。</td>
    </tr>
    <tr>
      <td><b>評等</b></td>
      <td>讓使用者能夠提供星級式評等。</td>
    </tr>
    <tr>
      <td><b>重設按鈕</b></td>
      <td>將表單欄位重設為其預設狀態。</td>
    </tr>
    <tr>
      <td><b>提交按鈕</b></td>
      <td>觸發表單提交並啟動定義好的工作流程。</td>
    </tr>
    <tr>
      <td><b>電話號碼欄位</b></td>
      <td>擷取具有國家/地區格式的電話號碼。</td>
    </tr>
    <tr>
      <td><b>文字</b></td>
      <td>提供專門的區段來顯示法律條款，並透過核取方塊取得使用者同意。</td>
    </tr>
    <tr>
      <td><b>文字欄位</b></td>
      <td>DCapture 擷取單行輸入，例如姓名或電子郵件地址。</td>
    </tr>
    <tr>
      <td><b>精靈</b></td>
      <td>引導使用者逐步完成多部分形式表單的流程。</td>
    </tr>
  </tbody>
</table>

<!-- * Footer: Adds a footer section for consistent design or additional information.
* Form Container: Wraps all form elements and manages overall form properties.
* Header: Adds a header section for form titles, branding, or instructions.-->
<!-- * 
* Prefillable Fields: Automatically populates form fields with data from predefined sources such as user profiles or APIs. 

* Switches/Toggle Buttons: Provides binary on/off choices for user input.


* Title: Adds a text-based heading or label to improve form clarity and organization.


In-addtion to pre-built form components, the Universal editor also provides support for:

* **Embedding Forms in Another Webpage**: The Universal Editor supports embedding forms directly into Edge Deliver Services Sites pages. This can be done using the embed component provided out of the box.

* **Validation Messages**: Validation messages provide real-time feedback to users when they enter incorrect or incomplete data. Features include:
    * Dynamic Error Display: Instantly alerts users to errors, such as invalid email addresses or missing required fields.
    * Customizable Messages: Allows form authors to define user-friendly error texts.
    * Rule-Based Validation: Supports advanced validation logic, such as checking dependencies between fields or implementing conditional rules.

* **Hidden Fields**: Hidden fields store data invisibly within the form, often for backend processing or prefilled values. Use cases include:
    * Passing contextual information (e.g., user ID or session data) to the backend without displaying it to users.
    * Capturing metadata like timestamps or tracking IDs.
    * Hidden fields are not visible to end-users but can be prefilled, updated dynamically, or used in workflows.

* **Custom Components**: Custom components allow developers to extend the functionality of forms by creating specialized or third-party integrations. Features include:
    * Flexibility: Developers can design unique form elements tailored to specific use cases.
    * Third-Party Integration: Embed widgets or tools like payment gateways, analytics trackers, or AI-driven input fields.
    * Seamless Compatibility: Custom components can integrate with the Universal Editor's drag-and-drop interface and existing features like data binding or validation.

* **Thank you Configuration**: Customize the acknowledgment message or page shown after form submission.
-->


## 上線

<span class="preview">這是一項預先發佈功能，可透過我們的<a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features">預先發佈管道</a>取得。</span>

## 常見問題集 (FAQ)

**問：誰可以使用通用編輯器？**
通用編輯器旨在供廣泛客群使用，包括：

* 想要建置具有視覺吸引力的表單的內容創作者。
* 需要進階自訂和整合功能的開發人員。
* 尋求可擴充、安全且合規的表單解決方案之組織。

**問：我可否將使用通用編輯器建立的表單整合至現有的系統中？**
當然可以。通用編輯器支援資料與後端系統無縫連結，以利即時更新和進階資料對應。通用編輯器亦與 Adobe Workfront 等工具整合以進行任務管理，並支援供資料提交工作流程使用的安全端點。

**問：可以自訂表單元件嗎？**
可以，通用編輯器可讓開發人員建立符合特定組織需求的自訂元件。此外，您可以透過使用者介面延伸模組和自訂工作流程來擴充編輯器的功能。

**問：通用編輯器如何滿足無障礙要求？**
通用編輯器的設計嚴格遵守無障礙標準，包括 WCAG (網頁內容無障礙指南)。這樣可以確保身心障礙人士可以使用這些表單，提供包容性體驗。

**問：我可以從表單中獲得哪類型的分析？**
通用編輯器包括內建分析和追蹤工具，用於監視使用者互動情形、表單提交率和轉換量度。這些深入分析有助於最佳化您的表單，以達到更好的效能。


## 開始建立表單

{{universal-editor-see-also}}

