---
title: 導覽 AEM Forms 的通用編輯器介面
description: 熟悉通用編輯器介面，以便建立搭配 Edge Delivery Services 的 AEM Forms。透過此全面性的介面指南了解基本工具、快速鍵和工作流程，以便提高建置表單的效率。
keywords: 通用編輯器, AEM forms, edge delivery services, 介面指南, 表單製作, WYSIWYG 編輯器, 表單產生器工具, 使用者介面導覽
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 07160248d5b5817d155a118475878ce04a687a32
workflow-type: tm+mt
source-wordcount: '2355'
ht-degree: 90%

---


# 導覽 AEM Forms 的通用編輯器介面

[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)提供視覺化介面，協助建立搭配 Edge Delivery Services 的 AEM Forms。它提供&#x200B;**What You See Is What You Get (WYSIWYG)**&#x200B;體驗，可精確顯示您的表單對使用者的顯示方式。

![通用編輯器介面概觀](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

本指南可協助您瞭解介面，以有效建置表單。 無論您初次建置表單或是經驗豐富的開發人員，本指南都將幫助您：

**學習基本技能：**

- 自信且有效率地導覽介面
- 使用適當的工具完成常見的表單建立任務
- 善用鍵盤快速鍵來提高生產力
- 常見介面問題疑難排解

**熟悉主要工作流程：**

- 設定工作區以達到最佳生產力
- 建置表單，從概念發想到出版物
- 在不同裝置上測試和預覽表單
- 與團隊成員協作完成表單專案



## 快速入門

**首次使用者：**&#x200B;從[基本工具](#essential-tools-for-form-building)開始了解最常使用的核心功能。

**經驗豐富的使用者：**&#x200B;跳至[進階功能](#advanced-features-and-integrations)，了解專用工具與整合。

**快速參考：**&#x200B;使用[介面概觀](#interface-overview)和[鍵盤快速鍵](#keyboard-shortcuts)區段來快速查詢。

>[!NOTE]
>
> 初次製作表單？請參閱 [AEM Forms 適用的 Edge Delivery Services 快速入門](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)，瞭解建立表單的逐步操作指南。

## 介面概觀

通用編輯器介面分為四個主要區域，每個區域皆有特定任務：

![通用編輯器介面的版面](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

| **區域** | **用途** | **主要用途** |
|----------|-------------|----------------|
| **[A：Experience Cloud 頁首](#experience-cloud-header)** | 導覽和帳戶管理 | 切換至不同的 Adobe 工具、存取說明、管理通知 |
| **[B：通用編輯器工具列](#universal-editor-toolbar)** | 表單編輯與發佈 | 建立、編輯、預覽和發佈表單 |
| **[C：屬性面板](#properties-panel)** | 元件設定 | 設定表單欄位、管理內容結構、存取進階功能 |
| **[D：編輯器版面](#editor-canvas)** | 透過視覺化方式建置表單 | 新增元件、安排版面、查看即時預覽 |

**介面流程：**&#x200B;大多數使用者主要在&#x200B;**編輯器版面** (D) 和&#x200B;**屬性面板** (C) 中操作，使用&#x200B;**工具列** (B) 來執行如預覽和發佈等動作。

## 表單建置的基本工具

如果您是初次使用通用編輯器，請從這裡開始。這些是多數表單建置任務都會用到的核心工具：

### **1. 編輯器版面：主要工作區**

**編輯器版面**&#x200B;是用視覺化方式建置表單的地方。此版面準確地顯示您的表單對使用者呈現的樣子。

![編輯器版面](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**關鍵動作：**

- 在屬性面板中按一下「**新增**」按鈕來&#x200B;**新增元件**。
- 在版面中直接點按各個元素來&#x200B;**選取元素**
- **在設定元件時查看即時變更**
- 在預覽模式中&#x200B;**測試互動**

### **2. 屬性面板 - 設定您的元件**

您可以在&#x200B;**屬性面板** (右側) 中自訂選取的元件及管理表單結構。

![屬性面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

**基本功能：**

- **屬性模式** (快速鍵 `d`) - 對所選取元件進行設定
- **內容樹** (快速鍵 `f`) - 導覽表單結構
- **新增元件** (快速鍵 `a`) - 插入新的表單欄位
- **元件動作** - 重複或刪除所選取元素

### **3. 工具列基本功能 - 預覽和發佈**

您可以使用&#x200B;**通用編輯器工具列**&#x200B;進行測試和發佈表單的關鍵動作。

![通用編輯器工具列](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

**必須知道的工具：**

- **預覽模式** (快速鍵 `p`) - 測試您的表單對使用者呈現的樣子
- **回應式模式** - 檢查表單在行動裝置上呈現的樣子
- **開啟頁面** (快速鍵 `o`) - 在新標籤中檢視表單
- **發佈** - 讓表單上線供使用者使用

### **4. 快速入門工作流程**

**您的第一份表單：**

1. **開始建置**：使用「**新增**」按鈕 (`a`) 新增元件
2. **設定欄位**：選取元件並使用&#x200B;**屬性模式** (`d`)
3. **測試表單**：使用&#x200B;**預覽模式** (`p`) 與表單進行互動
4. **檢查行動裝置視圖**：切換到&#x200B;**回應式模式**&#x200B;進行行動裝置測試
5. **上線**：準備好即可按一下「**發佈**」

**驗證查核點：**

- 您可以新增和設定表單欄位嗎？
- 預覽模式是否正確運作？
- 所有必填欄位是否皆設定正確？
- 表單在行動裝置上是否正常顯示？

## Experience Cloud 頁首

**Experience Cloud 頁首**&#x200B;提供導覽和帳戶管理工具。多數表單建置者偶爾使用此頁首來切換到不同的 Adobe 工具或是存取相關說明。

![Experience Cloud 頁首](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

**主要元素：**

| **元素** | **用途** | **何時使用** |
|-------------|-------------|----------------|
| **Adobe Experience Cloud** | 導覽至其他 Adobe 工具 | 在 Sites、Assets、Forms 之間切換 |
| **組織** | 切換至不同的組織 | 多個組織存取的情境 |
| **說明** | 存取文件與支援 | 當您需要指引或想要提交意見時 |
| **通知** | 檢視所指派的任務和警報 | 查看工作流程狀態 |
| **解決方案** | 快速存取其他 Adobe 解決方案 | 移動到不同的 Adobe 產品 |
| **使用者設定檔** | 帳戶設定和登出 | 管理帳戶或切換使用者 |

**最常見的用途：**

- **取得說明** - 按一下「說明」圖示以取得文件和支援
- **切換組織** - 如果您擁有多個組織的存取權，請使用「組織」下拉式選單

## 通用編輯器工具列

**通用編輯器工具列**&#x200B;包含主要的表單編輯和發佈工具。這些工具都是按照使用頻率和典型工作流程排列。

![通用編輯器工具列](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

### **日常工作流程工具**

**大多數表單建置過程都會使用以下工具：**

#### **預覽模式** (快速鍵 `p`)

**用途：**&#x200B;完全模擬使用者體驗，測試您的表單\
**何時使用：**&#x200B;發佈前、修改後、測試表單功能

![預覽模式](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

**最佳做法：**&#x200B;每次重大變更後都進行預覽，以儘早發現問題。

#### **回應式模式**

**用途：**&#x200B;檢查表單在行動裝置上的顯示方式\
**何時使用：**&#x200B;建置表單後、發佈前

![回應式模式](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

**最佳做法：**&#x200B;持續測試行動裝置視圖，因為許多使用者會透過手機存取表單。

#### **開啟頁面** (快速鍵 `o`)

**用途：**&#x200B;在沒有編輯器介面的新標籤中檢視表單\
**何時使用：**&#x200B;進行全螢幕測試，和利害關係人共用以供審閱

![開啟頁面](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

#### **發佈**

**用途：**&#x200B;讓表單上線且可供使用者存取\
**何時使用：**&#x200B;在預覽和回應式模式中完成全面測試之後

![發佈](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

**發佈前驗證檢查清單：**

- 已經在預覽模式下完成表單測試
- 已確認行動裝置回應能力
- 所有必填欄位均已設定
- 提交動作正常運作

### **導覽工具**

#### **首頁按鈕**

**用途：**&#x200B;返回通用編輯器開始頁面\
**何時使用：**&#x200B;開始處理其他表單

![首頁按鈕](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

#### **位置列** (快速鍵 `l`)

**用途：**&#x200B;透過 URL 直接導覽到任何表單\
**何時使用：**&#x200B;在特定表單之間快速切換

![位置列](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

### **進階設定工具**

**以下工具適合針對特定情境或進階設定使用：**

#### **AEM表單屬性**

**用途：**&#x200B;進行表單層級設定，例如表單資料模型 (FDM) 和出版日期\
**何時使用：**&#x200B;設定資料整合、安排出版時程

![表單屬性](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

![表單屬性精靈](/help/edge/docs/forms/universal-editor/assets/form-properties-ue.png)

「表單屬性」面板包含下列區段：

- **提交**：定義使用者提交表單後會發生什麼事。 從多個提交動作中進行選擇，例如透過電子郵件傳送資料、提交至SharePoint、使用表單資料模型，或整合Adobe Experience Platform或Microsoft Power Automate等服務。 如需支援提交動作的完整清單，請參閱[提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)文章。

- **預填**：設定使用者與表單互動前，表單欄位自動填入的方式。 您可以連線至表單資料模型(FDM)等資料來源，或使用URL引數預先填入欄位，增強使用者體驗並減少手動輸入。 若要深入瞭解，請參閱[預填服務](/help/edge/docs/forms/universal-editor/prefill-form.md)文章。

- **謝謝**：自訂使用者在提交表單後看到的內容。 您可以顯示確認訊息，或將訊息重新導向至其他網頁，確保順利且專業的完成體驗。 若要瞭解如何設定表單的感謝訊息，請參閱[設定感謝訊息](/help/edge/docs/forms/universal-editor/configure-thankyou-message.md)文章。

#### **規則編輯器** (搶先體驗)

**用途：**&#x200B;新增動態行為、驗證和條件式邏輯\
**何時使用：**&#x200B;建立具有複雜商業邏輯的互動式表單

![規則編輯器](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

>[!IMPORTANT]
>
> **搶先體驗功能：**&#x200B;規則編輯器需要特殊存取權。請聯絡 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 以啟用此功能。
>
> **了解更多：**&#x200B;請參閱[規則編輯器指南](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)以了解詳細說明。

#### **驗證標頭設定**

**用途：**&#x200B;設定自訂驗證標頭供開發測試使用\
**何時使用：**&#x200B;本機開發需驗證的表單

![驗證標頭](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

#### **其他選項** (省略符號選單)

**用途：**&#x200B;存取較少使用的動作，例如取消發佈\
**何時使用：**&#x200B;使表單離線、存取進階選項

![其他選項](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

## 屬性面板

**屬性面板** (右) 是建置和設定表單的控制中心。此面板會根據您選取的內容而變更，並為不同任務提供不同工具。

![屬性面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

### **核心表單建立工具**

**這些是建立和組織表單的基本工具：**

#### **新增元件** (快速鍵 `a`)

**用途：**&#x200B;插入新的表單欄位和元素\
**運作方式：**&#x200B;顯示所選取容器的可用元件

![新增元件](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

**常見元件：**

- 文字輸入、電子郵件、電話欄位
- 下拉式選單、選項按鈕、核取方塊
- 檔案上傳、日期挑選器
- 方便整理排列的面板和區段

#### **屬性模式** (快速鍵 `d`)

**用途：**&#x200B;進行選取元件設定\
**何時使用：**&#x200B;新增任何元件之後，以便自訂其行為

![屬性模式](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

**主要設定：**

- 欄位標籤和預留位置文字
- 驗證規則 (必填、格式、長度)
- 預設值和說明文字
- 條件式可見度規則

#### **內容樹** (快速鍵 `f`)

**用途：**&#x200B;導覽及整理排列表單結構\
**何時使用：**&#x200B;包含多個區段的複雜表單、尋找特定元件

![內容樹](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

**優點：**

- 快速導覽至任何元件
- 視覺化表單階層
- 輕鬆重新排列元素

#### **元件動作**

**用途：**&#x200B;管理現有元件\
**可用動作：**

- **重複** - 快速複製元件![重複](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)
- **刪除** - 移除元件 (無確認提示) ![刪除](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### **進階功能和整合**

**這些工具可以執行複雜的表單功能：**

+++資料整合

#### **資料來源**

**用途：**&#x200B;將表單連接到後端資料系統\
**何時使用：**&#x200B;需要讀取/寫入資料庫或外部服務的表單

![資料來源](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

**功能：**

- 表單資料模型 (FDM) 設定
- 動態資料群體
- 提交至外部系統

+++

+++AI支援工具

#### **產生變化版本**

**用途：**&#x200B;使用 AI 建立不同版本的表單內容\
**何時使用：**&#x200B;使用不同的文字、版面或方法進行實驗

    ![Generate Variations](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

**了解更多：**[產生變化版本指南](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

#### **內容草稿**

**用途：**&#x200B;建立並儲存初步文字版本\
**何時使用：**&#x200B;反覆修改表單副本、儲存替代文字選項

![內容草稿](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

+++

+++測試和最佳化

#### **A/B 測試**

**用途：**&#x200B;比較表單的變化版本以便實現最佳效能\
**何時使用：**&#x200B;最佳化轉換率、測試不同設計

![A/B 測試](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

#### **實驗**

**用途：**&#x200B;對表單設計進行受控測試\
**何時使用：**&#x200B;資料導向表單最佳化、使用者體驗測試

    ![Experimentation](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

+++

+++Collaboration工具

#### **任務管理**

**用途：**&#x200B;組織表單專案的團隊工作流程\
**何時使用：**&#x200B;多人表單開發、專案追蹤

![任務管理](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

#### **個人化**

**用途：**&#x200B;連接 Adobe Experience Platform 以便打造專屬體驗\
**何時使用：**&#x200B;根據使用者資料建立個人化表單

    ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

+++

## 編輯器版面

**編輯器版面**&#x200B;是以視覺化方式建置表單的主要工作區。此版面準確地顯示表單對使用者顯示的樣子，並在您進行更改時提供即時回饋。

![編輯器版面](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**主要功能：**

- **WYSIWYG 編輯** - 可立即查看所做的變更
- **直接互動** - 點按任何元件即可選取及編輯
- **即時預覽** - 切換到預覽模式來測試功能
- **回應式顯示** - 切換不同的裝置視圖以檢查行動裝置的相容性

**最佳做法：**

- **從結構開始** - 先新增主要區段，再加入詳細元件
- **頻繁測試** - 定期使用預覽模式，以儘早發現問題
- **優先考慮行動裝置** - 在整個設計過程中都要確認回應式模式

## 鍵盤快速鍵

熟悉這些快速鍵可以更快、更有效率地建置表單：

| **快速鍵** | **動作** | **何時使用** |
|--------------|------------|----------------|
| `a` | 開啟元件清單 | 新增表單欄位 |
| `d` | 開啟元件屬性 | 設定所選取元素 |
| `f` | 切換內容樹 | 導覽複雜表單 |
| `p` | 切換預覽模式 | 測試表單功能 |
| `o` | 在新標籤中開啟表單 | 全螢幕測試 |
| `l` | 將焦點移至位置列 | 切換到不同表單 |

**專業提示：**&#x200B;將這些快速鍵結合使用，例如選取一個元件，按下 `d` 進行設定，再按 `p` 測試相關變更。

## 常見工作流程

### **建立第一份表單**

1. **新增結構** - 使用 `a` 在表單區段中加入面板
2. **新增欄位** - 插入文字輸入、電子郵件和其他元件
3. **設定屬性** - 選取每個欄位並按 `d` 設定標籤和驗證
4. **測試功能** - 按 `p` 預覽及測試表單
5. **查看行動裝置視圖** - 使用回應式模式來確認行動裝置顯示的畫面
6. **發佈** - 準備好上線時按一下「發佈」

### **編輯現有表單**

1. **導覽結構** - 使用內容樹 (`f`) 快速找出元件
2. **選取並修改** - 直接點按元件或使用內容樹
3. **測試變更** - 每次完成重大變更後進行預覽 (`p`)
4. **驗證工作流程** - 重新發佈前先測試完整的表單流程

### **與團隊協作**

1. **使用任務管理** - 指派特定的表單區段給團隊成員
2. **共用以供審核** - 使用開啟頁面 (`o`) 來共用純粹的預覽畫面
3. **共同測試** - 使用預覽模式進行協作式測試作業
4. **追蹤進度** - 看查任務更新通知

## 常見問題疑難排解

### **介面問題**

+++介面元素未載入

**問題：**&#x200B;工具列按鈕、屬性面板或其他介面元素未顯示

**解決方案：**

- **重新整理頁面** - 通常只要瀏覽器重新整理就可以解決載入問題
- **檢查瀏覽器相容性** - 使用 Chrome、Firefox 或 Safari
- **清除瀏覽器快取** - 移除可能已過時的快取檔案
- **檢查權限** - 確保您擁有編輯表單的適當權限

+++

+++元件沒有回應

**問題：**&#x200B;無法選取元件或屬性面板未更新

**解決方案：**

- **直接點按元件** - 避免在空白區域點按
- **使用內容樹** - 按 `f` 並從內容樹選取元件
- **檢查是否有重疊元素** - 某些元件可能遮蔽其他元件
- **重新載入表單** - 使用位置列 (`l`) 重新載入目前表單

+++

+++預覽模式問題

**問題：**&#x200B;預覽模式無法正常運作或顯示錯誤

**解決方案：**

- **檢查表單驗證** - 確保所有必填欄位已正確設定
- **先在編輯模式下測試** - 在預覽前先確認元件都正常運作
- **清除瀏覽器快取** - 快取的指令碼可能影響預覽
- **檢查元件設定** - 審閱屬性模式的設定是否有錯誤

+++

## 提高表單建置效率的最佳做法

### **給組織的提示**

- **使用說明性名稱** - 在屬性模式下設定清楚的元件標籤
- **將相關欄位分組** - 使用面板依照邏輯組織表單區段
- **建置前先規劃** - 開始前先粗略勾勒出表單結構
- **保持簡單** - 避免使用過多欄位讓使用者感到不知所措

### **使用者體驗**

- **經常測試** - 每次進行重大變更後都要使用預覽模式
- **站在使用者的角度思考** - 考量完整的表單填寫體驗
- **提供清楚的標籤** - 讓使用者一眼看出每個欄位的用途
- **新增說明文字** - 針對複雜欄位提供說明文字

### **效能最佳化**

- **最小化元件** - 僅使用必要的表單欄位
- **最佳化影像** - 壓縮表單中使用的任何影像
- **在行動裝置上測試** - 確保使用較慢的行動連線時也有良好效能
- **儘早驗證** - 設定適當的驗證以避免提交錯誤

## 後續步驟

現在您已經了解通用編輯器介面：

1. **用簡單的表單練習** - 從基本欄位開始熟悉
2. **探索進階功能** - 做好準備後即可嘗試 AI 驅動的工具和整合
3. **學習表單製作** - 請參閱[快速入門手冊](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
4. **主要規則編輯器** - 使用[規則編輯器指南](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)新增動態行為

**請記住：**&#x200B;通用編輯器的目的是使表單建置變得直覺易用。從基本功能開始，再隨著需求成長逐步探索進階功能。
