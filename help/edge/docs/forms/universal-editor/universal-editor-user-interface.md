---
title: 導覽至AEM Forms的通用編輯器介面
description: 掌握通用編輯器介面，以使用Edge Delivery Services建立AEM Forms。 透過此全方位的介面指南，瞭解有效建置表單的基本工具、捷徑和工作流程。
keywords: 通用編輯器， AEM forms， edge delivery services，介面指南，表單製作， WYSIWYG編輯器，表單產生器工具，使用者介面導覽
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '2209'
ht-degree: 4%

---


# 導覽至AEM Forms的通用編輯器介面

[通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)提供使用Edge Delivery Services建立AEM Forms的視覺介面。 本指南可協助您瞭解介面，以有效建置表單。

![通用編輯器介面概觀](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## 概觀

Universal Editor提供&#x200B;**What You See Is What You Get (WYSIWYG)**&#x200B;體驗，可以向使用者顯示您表單的確切外觀。 無論您是剛開始建立表單，還是經驗豐富的開發人員，本指南都將協助您：

**學習基本技能：**

- 自信而有效地瀏覽介面
- 使用適當的工具執行常見的表單建立工作
- 利用鍵盤快速鍵提升生產力
- 疑難排解常見介面問題

**主要金鑰工作流程：**

- 設定您的工作區，以獲得最佳生產力
- 建立從概念到發佈的表單
- 跨裝置測試和預覽表單
- 與團隊成員在表單專案上共同作業

## 快速入門

**首次使用者：**&#x200B;從[基本工具](#essential-tools-for-form-building)開始，瞭解您最常使用的核心功能。

**經驗豐富的使用者：**&#x200B;跳至[進階功能](#advanced-features-and-integrations)，以進行專門工具與整合。

**快速參考：**&#x200B;使用[介面概觀](#interface-overview)和[鍵盤快速鍵](#keyboard-shortcuts)區段來快速查詢。

>[!NOTE]
>
> 不熟悉如何撰寫表單？ 如需逐步建立表單的指引，請參閱[AEM FormsEdge Delivery Services快速入門](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)。

## 介面概觀

Universal Editor介面分為四個主要區域，每個區域都針對特定工作而設計：

![通用編輯器介面配置](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

| **區域** | **用途** | **主要使用** |
|----------|-------------|----------------|
| **[A：Experience Cloud 標頭](#experience-cloud-header)** | 導覽與帳戶管理 | 在Adobe工具之間切換、存取說明、管理通知 |
| **[B：通用編輯器工具列](#universal-editor-toolbar)** | 表單編輯與發佈 | 建立、編輯、預覽和發佈表單 |
| **[C：屬性面板](#properties-panel)** | 元件設定 | 設定表單欄位、管理內容結構、存取進階功能 |
| **[D：編輯器畫布](#editor-canvas)** | 視覺化表單建置 | 新增元件、排列版面、檢視即時預覽 |

**介面流程：**&#x200B;大部分的使用者主要在&#x200B;**編輯器畫布** (D)和&#x200B;**屬性面板** (C)中工作，使用&#x200B;**工具列** (B)執行預覽和發佈等動作。

## 表單建立的基本工具

如果您是通用編輯器的新手，請從這裡開始。 這些是您用於大多數表單建置工作的核心工具：

### **1. 編輯器畫布 — 您的主要Workspace**

**編輯器畫布**&#x200B;是您以視覺化方式建立表單的地方。 它精確地顯示您的表單在使用者看來會是如何。

![編輯器畫布](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**主要動作：**

- 按一下屬性面板中的&#x200B;**新增**&#x200B;按鈕，即可新增元件&#x200B;****
- **選取元素**，方法是直接在畫布中按一下這些元素
- **在設定元件時檢視即時變更**
- 在預覽模式下測試&#x200B;**互動**

### **2. 屬性面板 — 設定您的元件**

**屬性面板** （右側）是您自訂選取元件和管理表單結構的位置。

![屬性面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

**基本功能：**

- **屬性模式** （`d`捷徑） — 設定選取的元件設定
- **內容樹狀結構** （`f`捷徑） — 導覽表單結構
- **新增元件** （`a`捷徑） — 插入新表單欄位
- **元件動作** — 複製或刪除選取的元素

### **3。 Toolbar Essentials — 預覽和發佈**

**通用編輯器工具列**&#x200B;提供測試和發佈表單的關鍵動作。

![通用編輯器工具列](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

**必須知道的工具：**

- **預覽模式** （`p`捷徑） — 測試您的表單，使用者可以看到它
- **回應模式** — 檢查您的表單在行動裝置上的外觀
- **開啟頁面** （`o`捷徑） — 在新索引標籤中檢視表單
- **發佈** — 讓您的表單對使用者上線

### **4。 快速入門工作流程**

**您的第一個表單：**

1. **開始建置** — 使用&#x200B;**新增**&#x200B;按鈕(`a`)新增元件
2. **設定欄位** — 選取元件並使用&#x200B;**屬性模式** (`d`)
3. **測試您的表單** — 使用&#x200B;**預覽模式** (`p`)與表單互動
4. **檢查行動檢視** — 切換至&#x200B;**回應模式**&#x200B;以進行行動測試
5. **上線** — 準備就緒時按一下&#x200B;**發佈**

**驗證檢查點：**

- 您可以新增及設定表單欄位嗎？
- 預覽模式是否正確運作？
- 所有必要欄位均已正確設定嗎？
- 表單在行動裝置上是否顯示良好？

## Experience Cloud 標頭

**Experience Cloud標題**&#x200B;提供導覽和帳戶管理工具。 大部分的表單建置者偶爾會使用它來在Adobe工具之間切換或存取說明。

![Experience Cloud標頭](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

**索引鍵元素：**

| **元素** | **用途** | **何時使用** |
|-------------|-------------|----------------|
| **Adobe Experience Cloud** | 導覽至其他Adobe工具 | 在網站、Assets、Forms之間切換 |
| **組織** | 在組織之間切換 | 多組織存取案例 |
| **說明** | 存取檔案和支援 | 當您需要指引或想提交意見回饋時 |
| **通知** | 檢視指派的任務和警示 | 檢查工作流程狀態 |
| **解決方案** | 快速存取其他Adobe解決方案 | 在不同的Adobe產品之間移動 |
| **使用者設定檔** | 帳戶設定和登出 | 管理帳戶或切換使用者 |

**最常見的使用：**

- **取得說明** — 按一下[說明]圖示以取得檔案與支援
- **切換組織** — 如果您有多重組織存取權，請使用組織下拉式清單

## 通用編輯器工具列

**通用編輯器工具列**&#x200B;包含您主要的表單編輯和發佈工具。 這些分類會依使用頻率和典型工作流程組織。

![通用編輯器工具列](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

### **每日工作流程工具**

**這些工具用於大多數的表單建立工作階段：**

#### **預覽模式** （`p`捷徑）

**用途：**&#x200B;請完全依照使用者體驗的方式測試您的表單\
**何時使用：**&#x200B;發佈之前（進行變更後）測試表單功能

![預覽模式](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

**最佳實務：**&#x200B;在每次重大變更後預覽，以及早發現問題。

#### **回應式模式**

**用途：**&#x200B;檢查您的表單在行動裝置上的顯示方式\
**使用時機：**&#x200B;建立表單後，發佈之前

![回應式模式](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

**最佳實務：**&#x200B;永遠測試行動裝置檢視 — 許多使用者會在手機上存取表單。

#### **開啟頁面** （`o`捷徑）

**用途：**&#x200B;在沒有編輯器介面的新索引標籤中檢視您的表單\
**何時使用：**&#x200B;若要進行全熒幕測試，請與利害關係人共用以進行檢閱

    ！[開啟頁面](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

#### **發佈**

**用途：**&#x200B;讓您的表單上線且可供使用者存取\
**使用時機：**&#x200B;在預覽和回應模式中進行徹底測試之後

    ！[發佈](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

發佈前&#x200B;**驗證檢查清單：**

- 在預覽模式下測試的表單
- 行動回應能力已驗證
- 所有必填欄位均已設定
- 提交動作正常運作

### **導覽工具**

#### **首頁按鈕**

**用途：**&#x200B;返回通用編輯器起始頁\
**何時使用：**&#x200B;開始處理其他表單

![首頁按鈕](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

#### **位置列** （`l`捷徑）

**用途：**&#x200B;透過URL直接導覽至任何表單\
**何時使用：**&#x200B;快速切換特定表單

![位置列](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

### **進階組態工具**

**這些工具用於特定案例或進階設定：**

#### **編輯表單屬性**

**用途：**&#x200B;設定表單層級設定，例如表單資料模型(FDM)和發佈日期\
**使用時機：**&#x200B;設定資料整合，排程發佈

![表單屬性](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

#### **規則編輯器** （可提早存取）

**用途：**&#x200B;新增動態行為、驗證和條件式邏輯\
**何時使用：**&#x200B;建立具有複雜商業邏輯的互動式表單

![規則編輯器](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

>[!IMPORTANT]
>
> **早期存取功能：**&#x200B;規則編輯器需要特殊存取權。 請連絡[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)以啟用此功能。
>
> **深入瞭解：**&#x200B;如需詳細指示，請參閱[規則編輯器指南](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)。

#### **驗證標頭設定**

**用途：**&#x200B;設定開發測試的自訂驗證標頭\
**何時使用：**&#x200B;需要驗證表單的本機開發

![驗證標頭](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

#### **其他選項** （省略符號選單）

**用途：**&#x200B;存取不常見的動作，例如取消發佈\
**何時使用：**&#x200B;將表單離線，存取進階選項

![其他選項](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

## 屬性面板

**屬性面板** （右側）是您建立和設定表單的控制中心。 它會根據您選取的內容而變更，並為不同工作提供不同的工具。

![屬性面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

### **核心表單建置工具**

**這些工具對於建立及組織您的表單至關重要：**

#### **新增元件** （`a`捷徑）

**用途：**&#x200B;插入新的表單欄位和元素\
**運作方式：**&#x200B;顯示所選容器的可用元件

![新增元件](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

**公用元件：**

- 文字輸入，電子郵件，電話欄位
- 下拉式清單、選項按鈕、核取方塊
- 檔案上傳，日期選擇器
- 組織的面板和區段

#### **屬性模式** （`d`捷徑）

**用途：**&#x200B;設定所選元件的設定\
**何時使用：**&#x200B;新增任何元件以自訂其行為之後

![屬性模式](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

**金鑰設定：**

- 欄位標籤和預留位置文字
- 驗證規則（必要、格式、長度）
- 預設值和說明文字
- 條件式可見性規則

#### **內容樹狀結構** （`f`捷徑）

**用途：**&#x200B;瀏覽並組織您的表單結構\
**何時使用：**&#x200B;包含多個區段的複雜表單，尋找特定元件

![內容樹](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

**優點：**

- 快速導覽至任何元件
- 視覺表單階層
- 輕鬆重新排序元素

#### **元件動作**

**用途：**&#x200B;管理現有元件\
**可用的動作：**

- **複製** — 快速複製元件![複製](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)
- **刪除** — 移除元件（無確認提示） ![刪除](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### **進階功能與整合**

**這些工具可啟用複雜的表單功能：**

+++資料整合

#### **資料來源**

**用途：**&#x200B;將表單連線至後端資料系統\
**何時使用：**&#x200B;需要讀取/寫入資料庫或外部服務的Forms

![資料來源](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

**功能：**

- 表單資料模型(FDM)設定
- 動態資料填入
- 提交至外部系統

+++

+++AI支援工具

#### **產生變化版本**

**用途：**&#x200B;使用AI建立不同版本的表單內容\
**何時使用：**&#x200B;嘗試不同的文字、版面配置或方法

    ！[產生變數](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

**深入瞭解：** [產生變數指南](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

#### **內容草稿**

**用途：**&#x200B;建立並儲存初步文字版本\
**何時使用：**&#x200B;重複表單復本，儲存替代文字選項

![內容草稿](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

+++

+++測試和最佳化

#### **A/B 測試**

**用途：**&#x200B;比較表單變數以最佳化效能\
**何時使用：**&#x200B;最佳化轉換率，測試不同的設計

![A/B 測試](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

#### **實驗**

**用途：**&#x200B;對表單設計執行受控測試\
**何時使用：**&#x200B;資料導向表單最佳化、使用者體驗測試

    ！[實驗](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

+++

+++Collaboration工具

#### **任務管理**

**目的：**&#x200B;組織表單專案的團隊工作流程\
**何時使用：**&#x200B;多人表單開發、專案追蹤

![任務管理](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

#### **個人化**

**用途：**&#x200B;與Adobe Experience Platform連線以提供量身打造的體驗\
**何時使用：**&#x200B;根據使用者資料建立個人化表格

    ！[Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

+++

## 編輯器畫布

**編輯器畫布**&#x200B;是您以視覺化方式建立表單的主要工作區。 它準確地顯示您的表單對使用者的顯示方式，並在您進行變更時提供即時意見回饋。

![編輯器畫布](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**主要功能：**

- **WYSIWYG編輯** — 在進行變更時立即檢視變更
- **直接互動** — 按一下任何元件以選取並編輯
- **即時預覽** — 切換到預覽模式以測試功能
- **回應式顯示器** — 切換裝置檢視以檢查行動裝置相容性

**最佳實務：**

- **以結構開始** — 在詳細元件之前新增主要區段
- **經常測試** — 定期使用預覽模式以及早發現問題
- **考慮行動優先** — 在整個設計過程中檢查回應模式

## 鍵盤快速鍵

掌握這些捷徑以更快更有效率地建立表單：

| **捷徑** | **動作** | **何時使用** |
|--------------|------------|----------------|
| `a` | 開啟元件清單 | 新增表單欄位 |
| `d` | 開啟元件屬性 | 設定選取的元素 |
| `f` | 切換內容樹狀結構 | 瀏覽複雜表單 |
| `p` | 切換預覽模式 | 測試表單功能 |
| `o` | 在新標籤中開啟表單 | 全熒幕測試 |
| `l` | 焦點位置列 | 切換至不同的表單 |

**專業秘訣：**&#x200B;組合使用這些捷徑 — 例如，選取元件，按`d`進行設定，然後按`p`測試變更。

## 常見工作流程

### **建立您的第一個表單**

1. **新增結構** — 使用`a`為表單區段新增面板
2. **新增欄位** — 插入文字輸入、電子郵件和其他元件
3. **設定屬性** — 選取每個欄位並按`d`以設定標籤和驗證
4. **測試功能** — 按`p`預覽及測試表單
5. **檢查行動檢視** — 使用回應式模式來驗證行動顯示
6. **發佈** — 準備上線時按一下[發佈]

### **編輯現有的Forms**

1. **瀏覽結構** — 使用內容樹狀結構(`f`)快速尋找元件
2. **選取並修改** — 直接按一下元件或使用內容樹狀結構
3. **測試變更** — 每次重大變更後預覽(`p`)
4. **驗證工作流程** — 重新發佈前請先測試完整的表單流程

### **與團隊合作**

1. **使用工作管理** — 指派特定表單區段給團隊成員
2. **共用檢閱** — 使用開啟頁面(`o`)共用乾淨的預覽
3. **一起測試** — 使用預覽模式進行協同合作測試工作階段
4. **追蹤進度** — 檢查任務更新的通知

## 疑難排解常見問題

### **介面問題**

+++介面元素未載入

**問題：**&#x200B;工具列按鈕、屬性面板或其他介面元素未出現

**解決方案：**

- **重新整理頁面** — 簡單的瀏覽器重新整理通常可解決載入問題
- **檢查瀏覽器相容性** — 使用Chrome、Firefox或Safari
- **清除瀏覽器快取** — 移除可能已過期的快取檔案
- **驗證許可權** — 確保您擁有編輯表單的適當存取權

+++

+++元件沒有回應

**問題：**&#x200B;無法選取元件或屬性面板未更新

**解決方案：**

- **直接按一下元件** — 避免按一下空白區域
- **使用內容樹狀結構** — 按下`f`並從樹狀結構選取元件
- **檢查重疊的元素** — 某些元件可能封鎖其他元件
- **重新載入表單** — 使用位置列(`l`)重新載入目前的表單

+++

+++預覽模式問題

**問題：**&#x200B;預覽模式無法正常運作或顯示錯誤

**解決方案：**

- **檢查表單驗證** — 確認所有必要欄位均已正確設定
- **先在編輯模式下測試** — 在預覽之前驗證元件是否有效
- **清除瀏覽器快取** — 快取的指令碼可能會干擾預覽
- **檢查元件組態** — 檢閱屬性模式設定是否有錯誤

+++

## 有效率表單建置的最佳實務

### **組織提示**

- **使用描述性名稱** — 在屬性模式中清楚標示元件
- **群組相關欄位** — 使用面板以邏輯方式組織表單區段
- **建置前先規劃** — 開始前先草繪您的表單結構
- **保持簡單** — 避免使用者過多欄位

### **效能最佳化**

- **最小化元件** — 僅使用必要的表單欄位
- **最佳化影像** — 壓縮表單中使用的任何影像
- **在行動裝置上測試** — 確保在較慢的行動連線上有良好的效能
- **及早驗證** — 設定正確的驗證以防止提交錯誤

### **使用者體驗**

- **經常測試** — 每次重大變更後都使用預覽模式
- **像使用者一樣思考** — 考慮完整的表單填寫體驗
- **提供清楚的標籤** — 讓使用者清楚瞭解欄位目的
- **新增實用文字** — 使用複雜欄位的說明文字

## 後續步驟

現在您已瞭解通用編輯器介面：

1. **使用簡單表單練習** — 從基本欄位開始，以熟悉使用
2. **探索進階功能** — 準備就緒後嘗試使用AI支援的工具和整合
3. **瞭解表單編寫** — 請參閱[快速入門手冊](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
4. **主規則編輯器** — 使用[規則編輯器指南](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)新增動態行為

**請記住：**&#x200B;通用編輯器的設計是要讓表單建置變得直覺化。 從基本功能開始，隨著您的需求增長，逐步探索進階功能。

