---
title: 如何建立多步驟表單序列？
description: 您可以利用  [!DNL Experience Manager Forms] 定義表單面板的序列，以便使用者導覽和填寫最適化表單。
role: User, Developer
level: Intermediate
feature: Adaptive Forms, Foundation Components
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 95%

---

# 多步驟表單序列簡介 {#introduction-to-multi-step-form-sequence}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/creating-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/introduction-form-sequence.html) |
| AEM as a Cloud Service  | 本文章 |

最適化表單可讓表單作者輕鬆建立多步驟資料擷取體驗。它隨附內建支援，可建立多個面板並將每個面板與不同的導覽模式建立關聯。表單作者可以在邏輯區段將表單欄位分組，並以面板來代表群組。面板之間的整體導覽是使用面板版面來控制。作者可以選擇以不同的版面配置來排列面板，例如，使用「精靈」版面配置以循序方式放置，或使用「索引標籤」版面配置以即興方式放置。 如需有關面板版面的資訊，請參閱[最適化表單的版面功能](layout-capabilities-adaptive-forms.md)。

在典型的表單填寫體驗中，所涉及的步驟並非只有擷取資料。完整的表單提交可能包括其他步驟，例如以數位方式在表單上簽名、驗證表單中填寫的資訊、處理付款等。具體情況因案例而異。

如果您的使用案例要求執行一組資料擷取步驟，或者有規定需要遵循特定步驟，[!DNL Experience Manager Forms] 提供了一種在表單間強制實施共同結構的方法。表單結構的預想實施會定義表單的步驟序列。![多步驟表單序列範例](assets/formpipeline.png)

多步驟表單序列範例

我們拿一個使用案例來舉例；在該案例中，您必須為表單建立填寫、驗證、簽名和確認步驟的序列。建立此類序列的步驟如下：

1. 定義表單範本並在其中新增所需的面板。序列中的每個步驟都應該有一個面板。但是，您可以在一個面板內包含子面板。

   在此範例中，我們可以新增以下面板：

   * **[!UICONTROL 填寫]**：包含用來擷取資料的表單欄位。您可以在這裡包含巢狀子面板，為不同資訊類型 (例如個人、家庭、財務等) 建立區段。

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL 電子簽署]**：包含可用於 XFA 型最適化表單的「**[!UICONTROL 簽名]**」元件。它提供以下簽署服務：

      * Adobe Document Cloud 電子簽署服務
      * 手寫簽名

   * **[!UICONTROL 確認]**：包含「**[!UICONTROL 摘要]**」元件，會在使用者簽署表單並到達序列中的「確認 (摘要)」步驟後，顯示確認表單提交的訊息。作者可以設定「[!UICONTROL 摘要]」元件的文字、顯示感謝訊息、顯示產生 PDF 的連結等等。

1. 選取根面板的版面做為「**[!UICONTROL 精靈]**」。
1. 完成其餘步驟即可建立表單範本。<!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

在表單範本中定義表單序列後，您可以將它用來建立具有定義為序列之基本結構的表單。不過，您隨時都可以自訂適合您要求的表單。


## 另請參閱 {#see-also}

{{see-also}}