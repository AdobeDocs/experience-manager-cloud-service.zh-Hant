---
title: 如何建立多步驟表單序列？
description: 使用 [!DNL Experience Manager Forms]，您可以定義表單面板的順序，供使用者導覽及填入最適化表單。 以使用案例方法為例，建立多步驟表單順序，以深入探討。
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# 多步驟表單序列簡介 {#introduction-to-multi-step-form-sequence}

適用性Forms可讓表單作者輕鬆建立多步驟資料擷取體驗。 內建支援可建立多個面板，並將每個面板與不同的導覽模式建立關聯。 表單作者可將邏輯區段中的表單欄位分組，並將群組表示為面板。 使用面板佈局控制面板之間的整體導航。 作者可以選擇以不同版面排列面板，例如使用「精靈」版面依序放置面板，或使用「標籤式版面」以臨機方式放置面板。 如需面板配置的相關資訊，請參閱 [適用性Forms的版面功能](layout-capabilities-adaptive-forms.md).

在一般的表單填寫體驗中，涉及的步驟不只是擷取資料。 完整的表單提交可包括其他步驟，例如以數位方式簽署表單、驗證表單中填入的資訊、處理付款等。 它不同個案。

如果您的使用案例要求執行資料擷取的一組步驟，或有需要執行特定步驟的法規， [!DNL Experience Manager Forms] 提供可跨表單強制執行此通用結構的方法。 表單結構的有預謀實施定義了表單的步驟順序。 ![多步驟表單序列範例](assets/formpipeline.png)

多步驟表單序列範例

讓我們舉個使用案例，說明您必須建立表單填寫、驗證、簽署和確認步驟的順序。 建立此類序列的步驟如下：

1. 定義表單範本，並新增必要的面板。 序列中的每個步驟都應有一個面板。 不過，您可以在面板內包含子面板。

   在此範例中，我們可新增下列面板：

   * **[!UICONTROL 填充]**:它包含用於擷取資料的表單欄位。 在此，您可以包含巢狀子面板，以針對不同類型的資訊（例如個人、家庭、財務等）建立區段。

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL 電子簽名]**:它包含 **[!UICONTROL Sign]** 可用於XFA型適用性表單的元件。 它提供下列簽署服務：

      * Adobe Document Cloud eSign Services
      * 手寫簽名
   * **[!UICONTROL 確認]**:它包含 **[!UICONTROL 摘要]** 元件，在使用者簽署表單並到達序列中的確認（摘要）步驟後，會顯示確認表單提交的訊息。 作者可以設定 [!UICONTROL 摘要] 元件、顯示感謝訊息、顯示產生PDF的連結等。



1. 選取根面板的版面配置為 **[!UICONTROL 精靈]**.
1. 完成其餘步驟以建立表單範本。 <!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

在表單模板中定義表單序列後，您可以使用它建立表單，該表單將基本結構定義為已定位的序列，但您始終可以定制表單以滿足您的要求。
