---
title: 如何使用 [!DNL Adobe Sign] 在自適應窗體中？
description: 您可以啟用電子簽名([!DNL Adobe Sign])自適應表單的工作流，以自動化簽名工作流、簡化單個和多簽名流程，以及從移動設備以電子方式簽名表單。
topic-tags: develop
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: cde9523e-5409-4edd-af0f-2c2575cc22ea
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '3100'
ht-degree: 1%

---


# 使用 [!DNL Adobe Sign] 在自適應窗體中 {#using-adobe-sign-in-an-adaptive-form}


>[!NOTE]
>
>在自適應表單中使用Adobe Sign角色的功能在2021年8月的預發行渠道中。 該功能將在2021年9月份上市。


[!DNL Adobe Sign] 可啟用最適化表單的電子簽名工作流程。 E-Signatures改進工作流以處理法律、銷售、工資、人力資源管理等領域的文檔。

典型 [!DNL Adobe Sign] 和自適應Forms方案，用戶填寫自適應表單以申請需要一個或多個方簽名的服務。 例如，申請抵押和信用卡需要所有借款人和共同申請人的合法簽名。 要為類似情形啟用電子簽名工作流，您可以整合 [!DNL Adobe Sign] 的下界。 還有幾個示例， [!DNL Adobe Sign] 至：

* 通過完全自動化的計畫書、報價和合同流程從任何設備處成交。
* 更快地完成人力資源流程並為您的員工提供數字型驗。
* 縮短合同週期，加快供應商的上架速度。
* 建立自動化常見流程的數字工作流。

[!DNL Adobe Sign] 整合 [!DNL AEM Forms] 支援：

* 單用戶和多用戶簽名工作流
* 連續和同時簽名工作流
* 以匿名用戶或登錄用戶身份簽名表單
* 動態簽名進程(與 [!DNL AEM Forms] 工作流)
* 通過知識庫、電話、社交檔案和政府ID進行身份驗證
* 將角色分配給每個協定收件人。 Adobe Sign的業務和企業服務級別可以選擇 [協定收件人角色](#addsignerstoanadaptiveform)。

<!-- * In-form and out-of-form signing experiences -->

## 必備條件 {#prerequisites}

使用前 [!DNL Adobe Sign] 在自適應窗體中：

* 確保 [!DNL AEM Forms] as a Cloud Service配置為使用Adobe Sign。 有關詳細資訊，請參閱 [將Adobe Sign與 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)。
* 讓收件人清單保持就緒。 您至少需要每個收件人的電子郵件地址。

## 配置 [!DNL Adobe Sign] 自適應窗體 {#configure-adobe-sign-for-an-adaptive-form}

配置 [!DNL Adobe Sign] 對於自適應表單：

1. [啟用 [!DNL Adobe Sign] 自適應窗體](#enableadobsignforanadaptiveform)
1. [添加 [!DNL Adobe Sign] 欄位到自適應窗體](#addadobesignfieldstoanadaptiveform)
1. [選擇 [!DNL Adobe Sign] Cloud Service自適應窗體](#select-adobe-sign-cloud-service-and-signing-order)

1. [添加 [!DNL Adobe Sign] 自適應表單的收件人](#addsignerstoanadaptiveform)
1. [為自適應表單選擇提交操作](#selectsubmitactionforanadaptiveform)

![收件人詳細資訊](assets/signer_details_new.png)

### 啟用 [!DNL Adobe Sign] 自適應窗體  {#enableadobesign}

您可以啟用 [!DNL Adobe Sign] 或建立 [!DNL Adobe Sign] 啟用的自適應窗體。 選擇以下選項之一：

* [建立 [!DNL Adobe Sign] 啟用的自適應窗體](#create-an-adaptive-form-for-adobe-sign)
* [啟用 [!DNL Adobe Sign] 用於現有自適應窗體](#editafsign)。

#### 為Adobe Sign建立自適應窗體 {#create-an-adaptive-form-for-adobe-sign}

要建立啟用符號的自適應表單：

1. 導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 點擊 **[!UICONTROL 建立]** 選擇 **[!UICONTROL 自適應窗體]**。 此時將顯示模板清單。 選擇模板並點擊 **[!UICONTROL 下一個]**。
1. 在 **[!UICONTROL 基本]** 頁籤：

   1. 指定 **[!UICONTROL 名稱]** 和 **[!UICONTROL 標題]** 的子菜單。

   1. 選擇 [配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 建立時 [整合 [!DNL Adobe Sign] 與 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)。
   配置容器包含 [!DNL Adobe Sign] Cloud Services已為您的環境配置。 這些服務可在Adaptive Form編輯器中進行選擇。

1. 在 **[!UICONTROL 窗體模型]** 頁籤中，選擇以下選項之一：

   * 如果您有自定義表單模板並需要基於表單模板的記錄文檔，請選擇 **[!UICONTROL 將表單模板與記錄文檔模板關聯]** 的子菜單。 使用此選項時，發送用於簽名的文檔只顯示基於關聯表單模板的欄位。 它不顯示自適應表單的所有欄位。

   * 如果沒有自定義表單模板，請選擇 **[!UICONTROL 生成記錄文檔]** 的雙曲餘切值。 使用此選項時，發送用於簽名的文檔將顯示自適應表單的所有欄位。

1. 點擊 **[!UICONTROL 建立。]** 建立啟用符號的自適應表單。 您可以添加 [!DNL Adobe Sign] 欄位，然後將其發送以進行簽名。

#### 啟用 [!DNL Adobe Sign] 自適應窗體 {#editafsign}

要使用 [!DNL Adobe Sign] 在現有的自適應窗體中：

1. 導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 選擇「自適應表單」並點擊 **[!UICONTROL 屬性]**。
1. 在 **[!UICONTROL 基本]** 頁籤 [配置容器](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 建立時間 [!DNL Adobe Sign] 與 [!DNL AEM Forms]。
1. 在 **[!UICONTROL 窗體模式]** 頁籤中，選擇以下選項之一：

   * 如果您有自定義表單模板並需要基於表單模板的記錄文檔，請選擇 **[!UICONTROL 將表單模板與記錄文檔模板關聯]** 的子菜單。 使用此選項時，發送用於簽名的文檔只顯示基於關聯表單模板的欄位。 它不顯示自適應表單的所有欄位。

   * 如果沒有自定義表單模板，請選擇 **[!UICONTROL 生成記錄文檔]** 的雙曲餘切值。 使用此選項時，發送用於簽名的文檔將顯示自適應表單的所有欄位。

1. 點擊 **[!UICONTROL 保存並關閉]**。 已為 [!DNL Adobe Sign]。 現在，您可以 [!DNL Adobe Sign] 欄位，然後將其發送以進行簽名。

### 添加 [!DNL Adobe Sign] 欄位到自適應窗體 {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] 具有可放置在「自適應表單」上的各個欄位。 這些欄位接受各種類型的資料，如簽名、縮寫、公司或標題，並幫助在簽名期間收集額外資訊以及簽名。 您可以使用 [!DNL Adobe Sign] 阻止要放置的元件 [!DNL Adobe Sign] 中各個位置的欄位。

要向自適應表單中添加欄位並定制與這些欄位相關的各種選項：

1. 拖放 **[!UICONTROL Adobe Sign街]** 元件從元件瀏覽器到自適應表單。 的 [!DNL Adobe Sign] 塊元件支援所有 [!DNL Adobe Sign] 的子菜單。 預設情況下，它會添加 **[!UICONTROL 簽名]** 的子菜單。

   ![標籤塊](assets/sign_block_new.png)

   預設情況下， [!DNL Adobe Sign] 塊在已發佈的自適應表單中不可見。 僅在簽名文檔中可見。 可以更改 [!DNL Adobe Sign] 阻止 [!DNL Adobe Sign] 阻止元件。

   >[!NOTE]
   >
   >  * 使用 [!DNL Adobe Sign] 塊不是強制使用的 [!DNL Adobe Sign] 的子菜單。 如果你不用 [!DNL Adobe Sign] 阻止和添加收件人的欄位，然後在簽名文檔底部顯示預設簽名欄位。
   >  * 使用 [!DNL Adobe Sign] 僅用於自動生成記錄文檔的Adaptive Forms。 如果使用自定義XDP生成記錄文檔或基於表單模板的自適應表單， [!DNL Adobe Sign] 不支援塊。



1. 選擇 **[!UICONTROL Adobe Sign街]** 並點擊 **[!UICONTROL 編輯]** ![編輯](assets/Smock_Edit_18_N.svg) 表徵圖 它顯示用於添加欄位和設定欄位外觀格式的選項。

   ![adobe符號塊選擇欄位](assets/adobe-sign-block-select-fields.png)

   **答：** 選擇並添加 [!DNL Adobe Sign] 的子菜單。 **B** 展開 [!DNL Adobe Sign] 阻止進入全屏視圖

1. 點擊 **[!UICONTROL Adobe Sign]** 欄位 ![Adobe Sign](assets/adobesign.png) 表徵圖 它顯示要選擇和添加的選項 [!DNL Adobe Sign] 的子菜單。

   展開 **[!UICONTROL 類型]** 下拉欄位以選擇 [!DNL Adobe Sign] 欄位並點擊「完成」 ![保存](assets/save_icon.svg) 表徵圖，將選定欄位添加到 [!DNL Adobe Sign] 框。 的 **[!UICONTROL 類型]** 下拉欄位包括「簽名」、「收件人資訊」和「資料」欄位類型。 [!DNL Adobe Sign] 集AEM成 [!DNL Forms] 中列出的支援欄位 [!UICONTROL 類型] 僅下拉框。 有關 [!DNL Adobe Sign] 欄位，請參閱 [Adobe Sign文檔](https://helpx.adobe.com/sign/help/field-types.html)。

   ![adobe符號塊欄位選項](assets/adobe-sign-block-fields-options.png)

   必須為欄位提供唯一名稱。 您也可以選擇必需選項來標籤必填欄位。 除 **[!UICONTROL 名稱]** 和 **[!UICONTROL 必需]** 選項，某些 [!DNL Adobe Sign] 選項。 例如，蒙版和多行。 此外，為每個名稱指定一個唯一名稱 [!DNL Adobe Sign] 欄位是否位於相同或不同 [!DNL Adobe Sign] 塊。

   如果選擇 **[!UICONTROL 數字簽名]** 從下拉清單中，可將數字簽名應用到「自適應表單」：

   * 使用雲簽名線上登錄 [數字身份證](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服務提供商托管。
   * 通過使用智慧卡、USB令牌或基於檔案的數字ID下載帶Adobe Acrobat或Reader的文檔進行本地下載。

### 啟用 [!DNL Adobe Sign] 自適應窗體 {#enableadobsignforanadaptiveform}

出局了， [!DNL Adobe Sign] 未為自適應窗體啟用。 要啟用它，請執行以下操作：

1. 在內容瀏覽器中，點擊 **[!UICONTROL 窗體容器]**，然後按一下 **[!UICONTROL 配置]** ![配置](assets/Smock_Wrench_18_N.svg) 表徵圖 它開啟屬性瀏覽器並顯示「自適應表單」容器屬性。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽名]** 折疊式，然後 **[!UICONTROL 啟用Adobe Sign]** 的雙曲餘切值。 它啟用 [!DNL Adobe Sign] 的子菜單。

### 選擇 [!DNL Adobe Sign] Cloud Service和簽名訂單 {#select-adobe-sign-cloud-service-and-signing-order}

可以配置多個 [!DNL Adobe Sign] 實例的服AEM務 [!DNL Forms]。 建議為每個職能（人力資源、財務等）單獨提供一套服務。 它使跟蹤和報告已簽署的文檔變得更容易。 例如，銀行有多個部門。 您可以為每個部門單獨配置以更好地跟蹤文檔。

文檔還可以具有多個收件人。 例如，信用卡申請可以具有多個申請人。 銀行在開始處理申請前需要所有申請人的簽名。 對於多收件人方案，您可以選擇按順序或同時順序對文檔進行簽名。

要選擇Cloud Service和簽名順序：

![雲服務](assets/cloud-service.png)

1. 在內容瀏覽器中，點擊 **[!UICONTROL 窗體容器]**，然後按一下 **[!UICONTROL 配置]** ![配置](assets/Smock_Wrench_18_N.svg) 表徵圖 它開啟屬性瀏覽器並顯示「自適應表單」容器屬性。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽名]** 折疊式，然後 **[!UICONTROL 啟用Adobe Sign]** 的雙曲餘切值。 它啟用 [!DNL Adobe Sign] 的子菜單。
1. 從已配置的Cloud Service清單中選擇 [!DNL Adobe Sign] Cloud Services。

   如果 **[!UICONTROL Adobe Sign Cloud Service]** 清單為空，請遵循 [配置 [!DNL Adobe Sign] 與 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md) 配置服務的文章。

   下拉清單中存在的Cloud Services `global` 「工具」>中的資料夾 **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**。 此外，下拉清單還列出了您在中選擇的資料夾中存在的Cloud Services **[!UICONTROL 配置容器]** 的子菜單。

1. 從 **[!UICONTROL 收件人可以完成]** 對話框。 收件人可以簽署自適應表單 **[!UICONTROL 順序]**  — 一個接一個的收件人，或 **[!UICONTROL 同時]**  — 按任意順序排列。

   按順序，一個接收方一次接收Adobe Sign協定。 接收方完成分配的操作後，協定將發送到下一個接收方，等等。

   同時，所有接受者都接受Adobe Sign協定，並可以相互平行地採取行動。

1. 使用協定ID欄位將二進位檔案與協定ID(agreementId)關聯。 它將協定ID添加到基於模式的表單的提交資料的afBoundData部分。 協定ID還添加到所有啟用Adobe Sign的表單的已提交資料中的afSubmissionInfo部分。 您可以使用協定ID來使用自定義代碼跟蹤協定狀態（需要自定義實施）。

1. [將收件人添加到自適應表單](working-with-adobe-sign.md#addsignerstoanadaptiveform) 點擊「完成」 ![保存](assets/save_icon.svg) 表徵圖。

### 將收件人添加到自適應表單 {#addsignerstoanadaptiveform}

您可以擁有一個或多個Adobe Sign協定收件人。 添加收件人時，您還可以為收件人配置身份驗證詳細資訊，並選擇表單填寫者和收件人是否是同一人。 執行以下步驟以添加和提供有關收件人的各種詳細資訊：

1. 在內容瀏覽器中，點擊 **[!UICONTROL 窗體容器]**，然後按一下 **[!UICONTROL 配置]** ![配置](assets/Smock_Wrench_18_N.svg) 表徵圖 它開啟帶有Adaptive Form容器屬性的屬性瀏覽器。
1. 在屬性瀏覽器中，展開 **[!UICONTROL 電子簽名]** 折疊式，然後 **[!UICONTROL 啟用Adobe Sign]** 的雙曲餘切值。 它啟用 [!DNL Adobe Sign] 的子菜單。
1. 點擊 **[!UICONTROL 添加收件人]**。 它將一個收件者添加到自適應表單中。 您可以將多個收件人添加到自適應表單。 所有接受者都收到Adobe Sign關於提交適應性表格的協定。
   ![電話詳細資訊](assets/recipient-settings.png)

1. 按一下 **[!UICONTROL 編輯]** ![編輯](assets/Smock_Edit_18_N.svg) 表徵圖以指定有關收件人的以下資訊：

   * **[!UICONTROL 標題]:** 指定標題以唯一標識收件人。

   * **[!UICONTROL 收件者和填表人是否相同?]:** 選擇 **[!UICONTROL 是]**，如果表單填寫者和第一收件人是同一人。 <!-- If the option is set to **No,** then do not use the signature step component in the Adaptive Form. If the form contains a Signature Step component, then the field is automatically set to Yes. -->

   * **[!UICONTROL 收件人角色]:** 選擇收件人的角色。 Adobe Sign的業務和企業服務級別可以選擇 [協定收件人角色](https://helpx.adobe.com/sign/using/set-up-signer-approver-roles.html)除了 **簽名者**，以更好地滿足其工作流要求。

   * **[!UICONTROL 收件人電子郵件地址]:** 指定收件人的電子郵件地址。 收件人收到指定電子郵件地址的Adobe Sign協定。 您可以選擇使用表單域中提供的電子郵件地址、登錄用戶的Experience Manager用戶配置檔案，或手動輸入電子郵件地址。 這是強制性的一步。

      >[!NOTE]
      >
      >確保第一個收件人或唯一收件人（如果有單個收件人）的電子郵件地址與 [!DNL Adobe Sign] 用於配置AEM雲服務的帳戶。

   * **[!UICONTROL 收件人認證方法]:** 指定在開啟Adobe Sign協定之前驗證收件人的方法。 您可以在電話、知識庫、基於社會身份的身份驗證和 [政府ID](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html)。
   >[!NOTE]
   >
   >    * 預設情況下，基於社會身份的身份驗證提供了使用Facebook、Google和LinkedIn進行身份驗證的選項。 您可以聯繫 [!DNL Adobe Sign] 支援以啟用其他社會身份驗證提供程式。


   * **[!DNL Adobe Sign]要填寫或簽名的欄位：** 選擇 [!DNL Adobe Sign] 的子菜單。 自適應表單可以具有多個 [!DNL Adobe Sign] 的子菜單。 您可以選擇為收件人啟用特定欄位。 該欄位顯示所有可用 [!DNL Adobe Sign] 阻止。 選擇塊時，塊的所有欄位都被選中。 可以使用X表徵圖取消選擇欄位。

   ![收件人詳細資訊](assets/signer-details.png)

   上圖有兩個示例 [!DNL Adobe Sign] 塊：個人資訊和辦公室詳細資訊

   點擊 ![保存](assets/save_icon.svg) 表徵圖 收件人已添加。

### 為自適應表單選擇提交操作 {#selectsubmitactionforanadaptiveform}

添加 [!DNL Adobe Sign] 欄位，啟用 [!DNL Adobe Sign] 從窗體容器中選擇 [!DNL Adobe Sign] Cloud Service，並添加Adobe Sign協定收件人，為自適應表單選擇相應的提交操作。 有關自適應Forms提交操作的詳細資訊，請參見 [配置提交操作](configuring-submit-actions.md)。

簽名和提交表單是相互獨立的。 在用戶提交表單後建立Adobe Sign協定後，即會提交自適應表單。 [!DNL AEM Forms] as a Cloud Service不會等待收件人簽署或完成其他操作以提交自適應表單。 一旦用戶按一下「提交」按鈕或「摘要」步驟顯示表單的摘要，即會提交表單。

另外， [!DNL Adobe Sign] 啟用的自適應表單嵌入Adobe Sign協定ID以提交資料。 您可以使用協定ID來使用自定義代碼跟蹤協定狀態（需要自定義實施）。

Adobe Sign協定ID(agreementId)包含在自適應表單的提交資料中。 預設情況下，協定ID位於 `afSubmissionInfo` 已提交資料的節點。

```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <afData>
      <afUnboundData>
         <data>
            <textbox1613455050902>ff</textbox1613455050902>
         </data>
      </afUnboundData>
      <afBoundData>
         <data xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" />
      </afBoundData>
      <afSubmissionInfo>
         <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].textbox1613455050902[0]</lastFocusItem>
         <stateOverrides />
         <signers>
            <signer0>
               <email />
            </signer0>
         </signers>
         <afPath>/content/dam/formsanddocuments/testsign</afPath>
         <afSubmissionTime>20210311031009</afSubmissionTime>
         <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
      </afSubmissionInfo>
   </afData>
```

（可選）您還可以將綁定與協定ID(agreementId)關聯。 它將協定ID添加到已提交資料的afBoundData節。 例如，在以下提交的資料中，協定ID綁定到 `<userName>` 節點：

```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <afData>
         <afUnboundData>
            <data />
         </afUnboundData>
         <afBoundData>
            <config xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
               <agreementID>3AAABLblqZhC2MWu7GFauKh45j_t2ih8mAtmbdIcNSl1HgQubhMJfDaDfylyN7NQiYRam_44ISKm45enIOafHqWZrdaxShf9r</agreementID>
               <dateOfBirth>0001-01-01</dateOfBirth>
            </config>
         </afBoundData>
         <afSubmissionInfo>
            <lastFocusItem>guide[0].guide1[0].guideRootPanel[0].projectDetails[0]</lastFocusItem>
            <stateOverrides />
            <signers>
               <signer0>
                  <email />
               </signer0>
            </signers>
            <afPath>/content/dam/formsanddocuments/testathon2021-1/gaurav/xsd-based</afPath>
            <afSubmissionTime>20210311095211</afSubmissionTime>
            <agreementId>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</agreementId>
         </afSubmissionInfo>
      </afData>
```

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the Adaptive Form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

您的表單簽名體驗已就緒。 您可以預覽表單以驗證簽名體驗。 在出版的表格上， [!DNL Adobe Sign] 當收件人收到通過電子郵件簽名的表單時，將顯示阻止欄位。 當 **[!UICONTROL 收件人和填寫表格的人何時相同？]** 選項被標籤為「是」並且符合條件，用戶在提交後將重定向到Adobe Sign協定，用戶可以立即簽署文檔，而不是等待協定出現在電子郵件中。

## 為自適應表單配置雲簽名 {#configure-cloud-signatures-for-an-adaptive-form}

基於雲的數字簽名或遠程簽名是新一代的數字簽名，可跨案頭、移動和Web工作，並滿足最高級別的合規性和收件人身份驗證保證。 您可以使用基於雲的數字簽名簽署自適應表單。

之後 [編輯適應窗體屬性Adobe Sign](working-with-adobe-sign.md#enableadobesign)，執行以下步驟將雲簽名欄位添加到自適應表單：

1. 拖放 **[!UICONTROL Adobe Sign街]** 元件從元件瀏覽器到自適應表單。 的 [!UICONTROL Adobe Sign街] 元件具有所有受支援的 [!DNL Adobe Sign] 的子菜單。 預設情況下，它會添加 **[!UICONTROL 簽名]** 的子菜單。

   ![標籤塊](assets/sign-block-new.png)

1. 選擇 **[!UICONTROL Adobe Sign街]** 並點擊 **[!UICONTROL 編輯]** ![編輯](assets/Smock_Edit_18_N.svg) 表徵圖 它顯示用於添加欄位和設定欄位外觀格式的選項。

   ![adobe符號塊選擇欄位](assets/adobe-sign-block-select-fields.png)

   **答：** 選擇並添加 [!DNL Adobe Sign] 的子菜單。 **B** 展開 [!DNL Adobe Sign] 阻止進入全屏視圖

1. 點擊 **[!UICONTROL Adobe Sign]** ![Adobe Sign](assets/adobesign.png) 表徵圖 它顯示要選擇和添加的選項 [!DNL Adobe Sign] 的子菜單。

   展開 **[!UICONTROL 類型]** 要選擇的下拉欄位 **[!UICONTROL 數字簽名]** 點擊 **[!UICONTROL 完成]** 表徵圖，將選定欄位添加到 [!DNL Adobe Sign] 框。

   ![數字簽名](assets/digital_signatures_new.png)

   必須為欄位提供唯一名稱。

   將數字簽名應用到自適應表單：

   * 雲簽名：使用 [數字身份證](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 由信任服務提供商托管。
   * Adobe Acrobat或Reader:下載並開啟帶有Adobe Acrobat或Reader的文檔，以使用智慧卡、USB令牌或基於檔案的數字ID進行簽名。

   將雲簽名欄位添加到自適應表單後，請執行以下步驟以完成配置過程：

   * [啟用Adobe Sign的自適應窗體](#enableadobsignforanadaptiveform)
   * [為自適應表單選擇Adobe Sign Cloud Service](#selectadobesigncloudserviceforanadaptiveform)
   * [將收件人添加到自適應表單](#addsignerstoanadaptiveform)
   * [為自適應表單選擇提交操作](#selectsubmitactionforanadaptiveform)


### 配置「感謝」頁或「摘要」步驟元件 {#configure-the-thank-you-page-or-summary-step-component}

的 **[!UICONTROL 摘要步驟]** 元件自動提交表單，填充自定義「摘要」頁面中的資訊，並顯示已提交表單的摘要。 「摘要步驟」(Summary Step)元件佔用窗體可用的全形。 建議在包含「摘要步驟」元件的部分上不使用任何其他元件。

## 常見問題 {#frequently-asked-questions}

**問：** 可以在另一個自適應表單中嵌入自適應表單。 嵌入的自適應表單 [!DNL Adobe Sign] 已啟用？
**答：** 不，Experience Manager Forms不支援使用嵌入了 [!DNL Adobe Sign] 已啟用用於簽名的自適應表單

**問：** 使用高級模板建立自適應表單並將其開啟進行編輯時，會出現錯誤消息「電子簽名或收件人配置不正確」。 的子菜單。 如何解決錯誤消息？
**答：** 使用高級模板建立的自適應表單配置為使用 [!DNL Adobe Sign]。 要解決錯誤，請建立並選擇 [!DNL Adobe Sign] 雲配置和配置 [!DNL Adobe Sign] 自適應表單的收件人。

**問：** 我能用 [!DNL Adobe Sign] 是否在自適應表單的靜態文本元件中設定文本標籤？
**答：** 是，可以在文本元件中使用文本標籤來添加 [!DNL Adobe Sign] 欄位到啟用自適應表單的「記錄文檔」（僅「自動生成的記錄文檔」選項）。 要瞭解建立文本標籤的過程和規則，請參見 [Adobe Sign文檔](https://helpx.adobe.com/sign/using/text-tag.html)。 另請注意，自適應Forms對文本標籤的支援有限。 可以使用文本標籤僅建立那些 [Adobe Sign街](working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) 支援。

## 疑難排解 {#troubleshoot}

### [!DNL Adobe Sign] 協定失敗 {#adobe-sign-agreement-failures}

**問題**
當 [!DNL Adobe Sign] 為Adaptive Form配置服務，該服務無法建立 [!DNL Adobe Sign] 協定。

**解析度**

* 檢查 [Adobe Sign Cloud Service](adobe-sign-integration-adaptive-forms.md) 在自適應窗體中使用。
* 確保API應用程式 [!DNL Adobe Sign] 用於配置的伺服器 [!DNL Adobe Sign] Cloud Service具有所需權限。
* 如果使用多個 [!DNL Adobe Sign] Cloud Services，指著 **[!UICONTROL 身份驗證URL]** 所有服務都一樣 **[!UICONTROL Adobe Sign·沙德]**。

* 使用單獨的電子郵件地址來配置 [!DNL Adobe Sign] 帳戶和第一個或單個收件人。 第一個收件人或唯一收件人（如果有單個收件人）的電子郵件地址不能與 [!DNL Adobe Sign] 用於配置AEM雲服務的帳戶。

## 相關文章 {#related-articles}

* [整合 [!DNL Adobe Sign] 與 [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md)
* [使用的最佳做法 [!DNL Adobe Sign] 與適應性Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
