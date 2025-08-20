---
title: 使用 Edge Delivery Services 建立和發佈自適應表單
description: 在AEM中使用Edge Delivery Services範本建立、編寫和發佈最適化Forms的逐步指示，著重於技術精確度和清晰度。
keywords: 調適型表單， edge delivery services，通用編輯器，表單建立， AEM forms，表單發佈
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 87%

---


# 使用 Edge Delivery Services 建立和發佈自適應表單

本檔案逐步說明如何使用AEM中的Edge Delivery Services範本建立、設定和發佈調適型Forms。 內容涵蓋從表單建立到生產部署的完整工作流程。

閱讀完本指南後，您將學會如何：

- 使用Edge Delivery Services範本建立表單
- 使用通用編輯器製作表單
- 設定表單並將表單發佈到 Edge Delivery Services
- 存取已發佈的表單及驗證部署



## 先決條件

在繼續操作前，請確保滿足以下先決條件：


- **AEM Forms as a Cloud Service**：擁有 Forms 授權的使用中作者實例。
- **GitHub 帳戶**：用於管理存放庫的個人或組織帳戶。
- **存放庫設定**：選擇以下其中一項：
   - **新專案**：[用自適應表單區塊建立新的 AEM 專案](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)該存放庫已針對 Edge Delivery Services 預先進行設定。
   - **現有專案**：[將自適應表單區塊新增至現有存放庫](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)並更新設定。

- **AEM-GitHub 連線**：在您的 AEM 實例和 GitHub 存放庫之間[建立連線](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)。
- **Edge Delivery Services**：確保存放庫已設定為自動部署。
- **權限**：請確認您具有建立和發佈表單所需的存取權。

- 確認 GitHub 存放庫包含自適應表單區塊。



## 表單建立和發佈工作流程

此流程包括三個主要階段：

- **階段1：** [表單建立](#step-1-form-creation)
- **第二階段：**[表單製作與設計](#step-2-form-authoring-and-design)
- **第三階段：**[設定與發佈](#step-3-configuration-and-publishing)

每個階段都包括確認設定是否正確的驗證步驟。


### 步驟1：建立表單

1. **存取表單建立功能**
   - 登入您的 AEM Forms as a Cloud Service 作者實例。
   - 導覽至「**Adobe Experience Manager**」>「**「表單**」>「**表單與文件**」。
   - 按一下「**建立**」>「**自適應表單**」。

1. **選取範本**
   - 在「**來源**」索引標籤中，選取一個&#x200B;**以 Edge Delivery Services 為基礎的範本**。
   - 「**建立**」按鈕變成啟用狀態。

     ![建立 EDS 表單](/help/edge/assets/create-eds-forms.png)

1. **設定選項 (選用)**
   - **「資料來源」標籤**：如有必要，請選取資料整合。
   - **「提交」標籤**：選擇提交動作 (可稍後設定)。
   - **「傳遞」標籤**：設定發佈/取消發佈的排程。

1. **完成表單設定**
   - 按一下「**建立**」來開啟表單建立精靈。
   - 輸入下列內容：
      - **名稱**：內部識別碼 (無空格，使用連字號)。
      - **標題**：表單的顯示名稱。
      - **GitHub URL**：存放庫 URL (例如 `https://github.com/your-org/your-repo`)。

   ![建立表單精靈](/help/edge/assets/create-form-wizard.png)

1. **驗證**
   - 按一下「**建立**」後，確認下列事項：
      - 表單在通用編輯器中開啟。
      - GitHub URL 已正確連結。
      - 元件面板可用。
      - 可以看到表單版面。

   ![通用編輯器介面](/help/edge/assets/author-form.png)

**結果：**&#x200B;表單已準備好，可以在通用編輯器中製作。

### 步驟 2：表單製作與設計


1. **存取元件庫**
   - 在通用編輯器中開啟內容瀏覽器。
   - 導覽至內容樹中的&#x200B;**自適應表單**&#x200B;元件。

   ![內容樹導覽](/help/edge/assets/content-tree.png)

1. **新增表單欄位**
   - 按一下「**新增**」圖示以開啟元件庫。
   - 在&#x200B;**自適應表單元件**&#x200B;清單中選取元件。
   - 將元件拖放到表單版面上。

   ![新增元件](/help/edge/assets/add-component.png)

1. **設計表單**
   - 在屬性面板中設定欄位屬性。
   - 設定驗證規則和行為。
   - 視需要調整樣式和版面。

   ![已填寫的註冊表單](/help/edge/assets/contact-us.png)

#### 驗證

- 所有必填欄位均存在。
- 欄位屬性已正確設定。
- 版面配置具備回應式與無障礙的特性。
- 驗證規則按預期運作。

#### 後續步驟

- 針對資料處理[設定提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)。
- [通用編輯器指南](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)說明進階功能。

### 步驟 3：設定與發佈

設定Edge Delivery Services並發佈您的表單。

**設定：**&#x200B;自動 (無需手動設定)。

- GitHub 存放庫連線以及 Edge Delivery Services 設定都在表單建立期間建立。
- 自動設定發佈端點。

**驗證：**

- 確認設定出現在表單設定中。
- 確保 GitHub URL 連結正確。

![自動 EDS 設定](/help/edge/assets/aem-instance-eds-configuration.png)

#### 發佈表單

1. 在通用編輯器中，按一下「**發佈**」按鈕 (右上角)。
2. 在對話框中確認發佈成功。
3. 請注意為中繼版本和即時版本產生的 URL。

   ![通用編輯器發佈](/help/edge/assets/publish-form.png)

- [發佈指南](/help/edge/docs/forms/universal-editor/publish-forms.md)

## 表單 URL

已發佈的表單可透過 Edge Delivery Services URL 存取。

### URL 結構

- **中繼 (預覽/測試)：**

  ```
  https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
  ```

- **即時 (生產)：**

  ```
  https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
  ```

#### URL 參數

- `<branch>`：GitHub 分支名稱 (例如 `main`、`develop`)
- `<repo>`：GitHub 存放庫名稱 (例如 `my-forms-project`)
- `<owner>`：GitHub 組織或使用者名稱 (例如 `company-name`)
- `<form_name>`：AEM 中定義的表單識別碼 (例如 `contact-us`)

#### 範例

組織 `acme-corp`之下存放庫 `forms-project` 中的表單 `contact-us` 之範例：

- **中繼：**`https://main--forms-project--acme-corp.aem.page/content/forms/af/contact-us`
- **即時：**`https://main--forms-project--acme-corp.aem.live/content/forms/af/contact-us`

#### 環境差異

- **中繼 (.page)：**&#x200B;用於測試的最新變更內容。
- **即時 (.live)：**&#x200B;用於生產的已發佈內容。

![URL 結構](/help/edge/docs/forms/universal-editor/assets/url-structure.svg)
*Edge Delivery Services 表單 URL 結構劃分*

#### 視覺化範例

**Edge Delivery Services 範本：**

- 中繼：![註冊表單的中繼版本](/help/forms/assets/registration-form-staged-version.png)
- 即時：![註冊表單的即時版本](/help/forms/assets/registration-form-live-version.png)

## 疑難排解

以下是搭配 Edge Delivery Services 的 AEM Forms 之常見問題和解決方案。

+++表單未載入

**問題：**&#x200B;表單 URL 傳回 404 或空白頁。

**解決方法：**

- 移除 URL 的 `.html` 副檔名。
- 確認表單已發佈。
- 檢查 GitHub 存放庫中的自適應表單區塊。
- 確保表單名稱與 URL 相符 (區分大小寫)。

+++

+++設定問題

**問題：** Edge Delivery Services 設定無法運作。

**解決方法：**

- 確保 GitHub URL 採用 `https://github.com/owner/repository` 格式。
- 在設定中使用正確的分支名稱。
- 驗證存放庫存取權 (公開或經過驗證)。
- 查看 `fstab.yaml` 以取得正確的 GitHub 詳細資訊。

+++

+++發佈問題

**問題：**&#x200B;變更內容未出現在即時網站上。

**解決方法：**

- 等待 2 至 3 分鐘，讓內容傳遞網路快取進行重新整理。
- 確認發佈工作流程已完成。
- 先在中繼 (.page) 環境中測試。
- 確保 GitHub 存放庫已更新。

+++

+++通用編輯器問題

**問題：**&#x200B;無法編輯表單或元件未載入。

**解決方法：**

- 使用支援的瀏覽器 (Chrome、Firefox、Safari)。
- 清除瀏覽器快取和 cookie。
- 驗證網路連線能力。
- 確認作者權限。

+++

+++表單提交錯誤

**問題：**&#x200B;表單提交無法運作。

**解決方法：**

- 在表單屬性中設定提交動作。
- 手動測試提交端點。
- 如果嵌入表單，請檢查 CORS 設定。
- 確認必填欄位均已設定。

+++

+++效能問題

**問題：**&#x200B;表單載入緩慢或效能不佳。

**解決方法：**

- 最佳化影像。
- 移除不必要的元件。
- 善用 Edge Delivery Services 內容傳遞網路。
- 盡量減少自訂 JavaScript/CSS 程式碼。

+++

+++取得協助

如果問題仍然存在：

1. 檢查 Adobe Experience Cloud 服務狀態。
2. 審閱 [Edge Delivery Services 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html)。
3. 造訪 [Adobe Experience League 社群](https://experienceleaguecommunities.adobe.com/?lang=zh-Hant)。
4. 聯絡 Adobe 客戶服務。

+++

## 後續步驟

表單建立和發佈完成後，請考慮以下事項：

- [設定提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)：設定資料處理和整合。
- [表單資料模型](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)：將表單連接到後端資料來源。
- [Edge Delivery Services 最佳做法](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/overview)：實現最大效能。
- [表單分析](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html)：追蹤表單效能和使用者行為。

