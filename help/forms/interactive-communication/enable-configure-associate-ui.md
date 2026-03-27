---
title: 啟用並設定互動式通訊的關聯UI
description: 瞭解如何啟用「關聯檢視」並設定互動式通訊設定中更新的工作流程，讓關聯者可以使用關聯UI。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 7c3e8a2b-5f21-4a1e-9e2d-8a4b6c7d8e9f
source-git-commit: a41459520feb03594212b91e68cfd8e2b1e610c4
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---

# 啟用並設定互動式通訊的關聯UI

>[!NOTE]
>
> 互動式通訊功能在早期採用者程式中提供。 使用您的工作郵件地址寄送電子郵件至 `aem-forms-ea@adobe.com` 請求存取權限。

本文說明如何為互動式通訊(IC)啟用關聯UI，以及選擇設定用於提交的AEM工作流程。 作者會在&#x200B;**互動式通訊設定**&#x200B;中執行這些步驟。

如需關聯UI和使用者角色的概觀，請參閱[互動式通訊編輯器中的關聯UI](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)。

## 先決條件

在啟用和設定關聯UI之前，請確定您已：

- **作者存取互動式通訊編輯器**。
- 已使用必要的配置與資料繫結建立&#x200B;**互動式通訊**。
- **關聯使用者**&#x200B;已新增至&#x200B;**forms-associates**&#x200B;群組（關聯者存取關聯UI所需）。
- **作者**&#x200B;已新增至&#x200B;**Forms-associates**&#x200B;群組（作者必須使用此群組才能存取關聯UI）。

當您準備好整合關聯UI與您的應用程式，並在發佈執行個體上叫用它時，您也將需要已啟用快顯視窗支援的瀏覽器並發佈互動通訊。 如需完整的整合必要條件，請參閱[在您的應用程式中整合關聯UI](/help/forms/interactive-communication/invoke-associate-ui.md)。

## 啟用關聯檢視（關聯UI）

在檔案層級啟用「關聯UI」 ，以便關聯者可以使用互動式通訊。

1. 在編輯器中開啟互動式通訊。
1. 從頂端動作列或檔案選項開啟&#x200B;**互動式通訊設定** （或&#x200B;**設定**）。

   ![互動式通訊設定 — 關聯屬性與啟用關聯檢視編輯](/help/forms/assets/associate-ui-settings.png)

1. 在左側面板中，確定已選取&#x200B;**關聯屬性**。
1. 在右側，核取&#x200B;**啟用關聯檢視編輯**。
1. 按一下&#x200B;**套用變更**，然後儲存檔案。

   ![互動式通訊設定 — 關聯屬性與啟用關聯檢視編輯](/help/forms/assets/associate-ui-enable-view.png)

訊息可能會提醒您套用變更並儲存檔案，以啟用「關聯檢視」。 儲存後，IC可用於關聯驅動使用。

### 允許為每個元件編輯關聯的UI

為IC啟用「關聯檢視」後，您必須針對關聯應該能夠編輯的每個元件，開啟&#x200B;**允許由關聯編輯**。 未開啟此設定的元件在關聯UI中會維持為唯讀。

1. 在IC編輯器中，在畫布或元件階層中選取元件（例如文字欄位）。
1. 在右側&#x200B;**屬性**&#x200B;面板中，展開&#x200B;**關聯屬性**。
1. 開啟&#x200B;**允許關聯編輯** **開啟**&#x200B;該元件。
1. 對關聯需要編輯的每個元件重複此動作，然後儲存檔案。

![允許在元件屬性中透過關聯進行編輯](/help/forms/assets/associate-ui-allow-editing-by-associate.png)

>[!NOTE]
>
> **關聯屬性**&#x200B;也包含&#x200B;**印刷樣式** （關聯UI中欄位的字型、大小和樣式）、**工具提示**&#x200B;和&#x200B;**模式** （驗證）等選項。 使用這些選項來控制關聯編輯元件時元件的外觀和行為 — 例如，設定驗證模式，讓關聯以所需格式輸入資料。

## 設定關聯UI的工作流程

若要在使用者從關聯UI提交或更新資料時執行AEM工作流程，請設定下列專案：

1. 在&#x200B;**互動式通訊設定**&#x200B;中，選取左側面板（在[關聯屬性]下）中的&#x200B;**工作流程**。
1. 開啟&#x200B;**設定更新**&#x200B;的工作流程&#x200B;**於**。
1. 在&#x200B;**選取工作流程模型**&#x200B;中，選擇要執行的AEM工作流程模型（例如`conversionWorkflow`或路徑，例如`/var/workflow/models/submit-workflow-1`）。
1. 選擇性地設定&#x200B;**工作流程成功訊息** （在工作流程完成之後顯示給使用者）。
1. 可選擇設定&#x200B;**重新導向URL**，在提交後傳送使用者至特定頁面。
1. 按一下&#x200B;**套用變更**&#x200B;並儲存檔案。

   ![互動式通訊設定 — 關聯UI的工作流程組態](/help/forms/assets/associate-ui-configure-workflow.png)

當您啟用工作流程時，它會在使用者從「關聯UI」提交時執行。 有關提交和工作流程的工作方式 — 執行位置、使用哪個執行個體以及關鍵考量，請參閱[關聯UI的提交工作流程](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior)。 該文章也包含從IC提交產生PDF的工作流程範例。

## 完成關聯UI設定

啟用「關聯檢視」並選擇性地設定工作流程後：

1. **啟用可編輯的欄位：**&#x200B;在IC的必要區段中，啟用關聯允許編輯的欄位。 視需要設定驗證和強制/唯讀行為。
1. **發佈IC**，使其可用於關聯的發佈執行個體。
1. 與關聯者共用已發佈的IC連結。 他們進行驗證（例如，透過[Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)）並開啟關聯UI、輸入或確認客戶資料，以及產生最終通訊。 如果您已設定工作流程，它會在提交時執行。 如需提交和工作流程如何運作，請參閱[關聯UI的提交工作流程](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior)。

## 另請參閱

- [在互動式通訊編輯器中建立UI關聯](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [在您的應用程式中整合關聯UI](/help/forms/interactive-communication/invoke-associate-ui.md)
- [關聯UI的提交工作流程 — IC產生PDF輸出](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md) — 提交和工作流程如何運作，加上從IC提交產生PDF的範例工作流程。
