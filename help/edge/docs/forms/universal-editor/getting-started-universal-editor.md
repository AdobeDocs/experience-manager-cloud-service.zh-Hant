---
title: 使用通用編輯器開始使用 AEM Forms 適用的 Edge Delivery Services
description: 了解如何使用通用編輯器的 WYSIWYG 製作功能來建立和發佈使用 Edge Delivery Services 的高效能表單。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '2609'
ht-degree: 68%

---


# 使用通用編輯器開始使用 AEM Forms 適用的 Edge Delivery Services

| 製作方法 | 指南 |
|---------------------------------|-----------------------------------------------------------------------|
| **通用編輯器 (WYSIWYG)** | 本文章 |
| **文件型製作** | [文件型教學課程](/help/edge/docs/forms/tutorial.md) |

AEM Forms 適用的 Edge Delivery Services 將高效能網頁傳遞與通用編輯器中的 WYSIWYG 製作功能結合。本指南說明建立、自訂和發佈快速載入表單。

## 您會學到什麼

完成本教學課程後，您將能夠：

- 使用自適應表單區塊設定 GitHub 存放庫
- 建立與 Edge Delivery Services 整合的 AEM 網站
- 使用通用編輯器建置和發佈表單
- 設定本機開發環境

## 選擇您的路徑

根據您的情境選取方法：

![選擇您的路徑決策指南](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*圖：幫助您選擇正確實施路徑的視覺化指南*

| **路徑 A：新專案** | **路徑 B：現有專案** |
|----------------------------------------|-------------------------------------------|
| 從預先設定的範本開始 | 將表單新增至目前的 AEM 專案 |
| **最適合：**&#x200B;新實施 | **最適合：**&#x200B;現有 AEM Sites |
| **您會得到：**&#x200B;預先設定的表單區塊 | **您會得到：**&#x200B;表單已新增至現有網站 |
| **步驟：**&#x200B;範本 → 設定 → 表單 | **步驟：**&#x200B;整合 → 設定 → 表單 |
| [從路徑 A 開始](#path-a-create-new-project-with-forms) | [從路徑 B 開始](#path-b-add-forms-to-existing-project) |

## 先決條件

為確保使用通用編輯器在AEM Forms中能順暢而成功地使用Edge Delivery Services，在繼續之前，請檢閱並確認下列必要條件：

### 存取要求

- **GitHub帳戶**：您必須擁有有權建立新存放庫的GitHub帳戶。 這對於管理您的專案原始程式碼以及與團隊合作至關重要。
- **AEM as a Cloud Service編寫存取權**：請確定您擁有AEM as a Cloud Service環境的作者層級存取權。 建立、編輯和發佈表單需要此存取權。

### 技術要求

- **熟悉Git**：您應該已熟悉如何執行基本的Git作業，例如複製存放庫、提交變更和推送更新。 這些技能是原始檔控制和專案共同作業的基礎。
- **瞭解Web技術**：建議您先瞭解HTML、CSS和JavaScript等實用知識。 這些技術構成了表單自訂和疑難排解的基礎。
- **Node.js （版本16或更新版本）**：本機開發和執行組建工具需要Node.js。 確定您的系統上已安裝版本16或更新版本。
- **封裝管理員（npm或yarn）**：您需要npm （Node封裝管理員）或yarn來管理專案相依性和指令碼。

### 建議的背景

- **AEM Sites概念**：對AEM Sites的基本瞭解（包括網站結構和內容製作）可協助您有效導覽和整合表單。
- **表單設計原則**：熟悉表單設計的最佳實務（例如可用性、協助工具及資料驗證）可讓您建立有效且方便使用的表單。
- **使用WYSIWYG編輯器的體驗**：先前使用What You See Is What You Get (WYSIWYG)編輯器的體驗，可協助您更有效率地運用通用編輯器的視覺化撰寫功能。

>[!TIP]
>
> 初次使用 AEM？從 [AEM Sites 快速入門手冊](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/sites/authoring/quick-start)開始。

## 路徑A：使用Forms建立新專案

**建議用於：**&#x200B;新專案、試行方案或概念證明方案

運用AEM Forms範本加速您的專案設定。 此範本提供立即可用的範本，可順暢地整合最適化Forms區塊，讓您在AEM網站中快速建立及部署表單。

### 概觀

若要成功啟動具有整合式表單的新專案，您將：

1. 使用AEM Forms範本建立GitHub存放庫。
2. 設定AEM程式碼同步，以自動化AEM與存放庫之間的內容同步。
3. 設定GitHub專案與AEM環境之間的連線。
4. 建立並發佈新的AEM網站。
5. 使用通用編輯器新增及管理表單。

以下各節將詳細引導您完成每個步驟，以確保流暢而有效的專案設定體驗。

+++步驟1：從範本建立GitHub存放庫

1. **存取 AEM Forms 樣板專案範本**
   - 前往 [https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)

   ![AEM Forms 樣板專案範本](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *圖：含有預先設定的自適應表單區塊的 AEM Forms 樣板專案存放庫*

2. **建立您的存放庫**
   - 按一下「**使用此範本**」>「**建立新存放庫**」。

   ![使用範本建立存放庫](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *圖：使用範本建立新的存放庫*

3. **設定存放庫**
   - **所有者**：選取您的 GitHub 帳戶或組織
   - **存放庫名稱**：選擇一個說明性名稱 (例如 `my-forms-project`)
   - **可見度**：選取「**公開**」(Edge Delivery Services 建議使用)
   - 按一下「**建立存放庫**」

   ![存放庫設定](/help/edge/docs/forms/assets/name-eds-repo.png)
   *圖：將新存放庫的可見度設為公開*

**驗證：**&#x200B;確認您擁有以 AEM Forms 樣板專案範本為基礎的新 GitHub 存放庫。

+++

+++步驟2：安裝AEM程式碼同步

AEM Code Sync 會自動同步您的 AEM 製作環境和 GitHub 存放庫之間的內容變更。

1. **安裝 GitHub 應用程式**
   - 前往 [https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)

2. **設定存取權限**
   - 選取「**僅選取存放庫**」
   - 選擇您新建立的存放庫
   - 按一下「**儲存**」

   ![安裝 AEM Code Sync](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *圖：安裝 AEM Code Sync 並有特定存放庫的權限*

**查核點：** AEM Code Sync 現已安裝並可存取您的存放庫。

+++

+++步驟3：設定AEM整合

`fstab.yaml`檔案將您的 GitHub 存放庫連接到 AEM 製作環境以進行內容同步。

1. **導覽到您的存放庫**
   - 前往新建立的 GitHub 存放庫
   - 您應該會看到 AEM Forms 樣板專案檔案

2. **建立 fstab.yaml 檔案**
   - 在根目錄中按一下「**新增檔案**」>「**建立新檔案**」
   - 將檔案命名為 `fstab.yaml`

   ![建立 fstab.yaml 檔案](/help/edge/docs/forms/assets/open-fstab.png)
   *圖：建立 fstab.yaml 設定檔案*

3. **新增您的 AEM 連線詳細資訊**

   複製貼上以下設定，取代預留位置：

   ```yaml
   mountpoints:
     /: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
   ```

   **取代：**
   - `<aem-author>`：您的 AEM as a Cloud Service 作者 URL (例如 `author-p12345-e67890.adobeaemcloud.com`)
   - `<owner>`：您的 GitHub 使用者名稱或組織
   - `<repository>`：您的存放庫名稱

   **範例：**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![編輯 fstab.yaml 檔案](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *圖：設定 AEM 整合的掛載點*

4. **認可設定**
   - 新增認可訊息：「新增 AEM 整合設定」
   - 按一下「**認可新檔案**」。

   ![認可 fstab 變更](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *圖：認可 fstab.yaml 設定*

**驗證：**&#x200B;確認您的 GitHub 存放庫與 AEM 的連線。

    >[！NOTE]
    >
    >有建置問題嗎？請參閱[疑難排解 GitHub 建置問題](#troubleshooting-github-build-issues)

+++

+++步驟4：建立連線至您GitHub存放庫的AEM網站。

1. **存取 AEM Sites 控制台**
   - 登入您的 AEM as a Cloud Service 製作實例。
   - 導覽至「**Sites**」

   ![AEM Sites 控制台](/help/edge/assets/select-sites.png)
   *圖：存取 AEM Sites 控制台*

2. **開始建立網站**
   - 按一下「**建立**」>「**使用範本建立網站**」。

   ![建立網站選項](/help/edge/docs/forms/assets/create-sites.png)
   *圖：使用範本建立新網站*

3. **選取 Edge Delivery Services 範本**
   - 選擇 **Edge Delivery Services 網站**&#x200B;範本
   - 按一下「**下一步**」。

   ![網站範本選取](/help/edge/docs/forms/assets/select-site-template.png)
   *圖：選取 Edge Delivery Services 網站範本*

   >[!NOTE]
   >
   >**範本無法使用？** 如果您沒有看到 Edge Delivery Services 範本：
   >
   >1. 請按一下「**匯入**」來上傳範本
   >2. 從 [GitHub 發行版本](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)下載範本

4. **設定您的網站**

   輸入下列資訊：

   | 欄位 | 值 | 範例 |
   |-----------------|-----------------------------|-----------------------------------------|
   | **網站標題** | 網站的說明性名稱 | 「我的表單專案」 |
   | **網站名稱** | URL 易記名稱 | 「my-forms-project」 |
   | **GitHub URL** | 您的存放庫 URL | `https://github.com/mycompany/my-forms-project` |

   ![網站設定](/help/edge/docs/forms/assets/create-aem-site.png)
   *圖：設定新的 AEM 網站並整合 GitHub*

5. **完成網站建立**
   - 審閱您的設定
   - 按一下「**建立**」。

   ![確認建立網站](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *圖：確認建立網站*

   **成功！**&#x200B;您的 AEM 網站現已建立並連線至 GitHub。

6. **在通用編輯器中開啟**
   - 在 Sites 控制台中，找到您的新網站
   - 選取 `index` 頁面
   - 按一下「**編輯**」

   ![在通用編輯器中編輯網站](/help/edge/docs/forms/assets/edit-site.png)
   *圖：開啟您的網站進行編輯*

   通用編輯器在新標籤中開啟，提供 WYSIWYG 製作功能。

   ![通用編輯器介面](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *圖：您的網站已在通用編輯器中開啟，以進行 WYSIWYG 編輯*

**驗證：**&#x200B;確認您的 AEM 網站已準備好進行表單製作。

+++

+++步驟5：發佈您的網站

發佈後，您的網站可以在 Edge Delivery Services 上供全球存取。

1. **從 Sites 控制台快速發佈**
   - 返回 AEM Sites 控制台
   - 選取您的網站頁面 (或使用 Ctrl+A 選擇全部)
   - 按一下「**快速發佈**」

   ![發佈 AEM 網站](/help/edge/docs/forms/assets/publish-sites.png)
   *圖：選取要快速發佈的頁面*

2. **確認發佈**
   - 在確認對話框中，按一下「**發佈**」

   ![快速發佈對話框](/help/edge/docs/forms/assets/quick-publish.png)
   *圖：確認發佈動作*

   **替代方案：**&#x200B;您也可以使用發佈按鈕直接從通用編輯器發佈。

   ![從通用編輯器發佈](/help/edge/docs/forms/assets/qui.png)
   *圖：從通用編輯器直接發佈*

3. **存取您的上線網站**

   您的網站現已上線：

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **URL 結構說明：**
   - `<branch>`：GitHub 分支 (通常為 `main`)
   - `<repo>`：您的存放庫名稱
   - `<owner>`：您的 GitHub 使用者名稱或組織
   - `<site-name>`：您的 AEM 網站名稱

   **範例：**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

**驗證：** 確認您的網站已在 Edge Delivery Services 上線。

>[!TIP]
>
> **URL 模式：**
>
> - **首頁：**`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **其他頁面：**`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**下一步：**&#x200B;[建立第一份表單](#create-your-first-form)

+++

## 路徑 B：將表單新增至現有專案

**最適合：**&#x200B;使用 Edge Delivery Services 的現有 AEM Sites

如果您已經有使用 Edge Delivery Services 的 AEM 專案，則可以透過整合自適應表單區塊來新增表單功能。

### 路徑 B 的先決條件

若要繼續將表單整合至您現有的AEM專案，請確定符合下列必要條件：

- 您有使用[AEM指令碼XWalk](https://github.com/adobe-rnd/aem-boilerplate-xwalk)建立的現有AEM專案。
- 您已設定[本機開發環境](#set-up-local-development-environment)
- 您擁有專案存放庫的Git存取權，可讓您視需要複製、修改和推送變更。

>[!NOTE]
>
> 如果您的專案最初是使用[AEM Forms樣板](https://github.com/adobe-rnd/aem-boilerplate-forms)設定的，則已包含表單功能。 在此情況下，您可以繼續前往[建立您的第一個表單](#create-your-first-form)區段。

下列指南提供將表單功能新增至現有專案的結構化方法。 每個步驟都旨在確保在Universal Editor環境中緊密整合和最佳功能。

### 概觀

您將完成下列高階步驟：

1. 將最適化Forms區塊檔案複製到專案中。
2. 更新專案的設定，以辨識及支援表單元件。
3. 調整ESLint規則以容納新的檔案和編碼模式。
4. 建置專案並將變更提交至您的存放庫。

+++步驟1：複製Forms區塊檔案

1. **導覽到您的本機專案**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **從 AEM Forms 樣板專案下載必要檔案**

   從 [AEM Forms 樣板專案存放庫](https://github.com/adobe-rnd/aem-boilerplate-forms)複製以下檔案：

   | 來源 | 目的地 | 用途 |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | 核心表單功能  |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | 通用編輯器整合 |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | 編輯器樣式 |

3. **更新編輯器支援**
   - 用 [AEM Forms 樣板專案中的 editor-support.js ](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)取代 `/scripts/editor-support.js` 檔案

**驗證：**&#x200B;確認表單區塊檔案在您的專案中。

+++

+++步驟2：更新元件設定

1. **更新區段模型**

   開啟 `/models/_section.json` 並將表單元件新增至篩選器：

   ```json
   {
        "filters": [
        {
      "id": "section",
      "components": [
           "text",
           "image",
           "button",
        "form",
        "embed-adaptive-form"
      ]
       }
     ]
   }
   ```

   **其作用：**&#x200B;在通用編輯器元件選擇器中啟用表單元件。

**驗證：**&#x200B;確認表單元件出現在通用編輯器中。

+++

+++步驟3：設定ESLint （選用）

**為什麼執行此步驟：**&#x200B;防止來自表單特定檔案的 linting 錯誤並設定適當的驗證規則。

1. **更新 .eslintignore**

   將這幾行加入 `/.eslintignore`：

   ```bash
   # Form block rule engine files
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

2. **更新 .eslintrc.js**

   將這些規則加入 `/.eslintrc.js` 中的 `rules` 物件：

   ```javascript
   {
     "rules": {
       // Existing rules...
   
       // Form component cell limits
    'xwalk/max-cells': ['error', {
         '*': 4, // default limit
      form: 15,
      wizard: 12,
      'form-button': 7,
      'checkbox-group': 20,
      checkbox: 19,
      'date-input': 21,
      'drop-down': 19,
      email: 22,
      'file-input': 20,
      'form-fragment': 15,
      'form-image': 7,
      'multiline-input': 23,
      'number-input': 22,
      panel: 17,
      'radio-group': 20,
      'form-reset-button': 7,
      'form-submit-button': 7,
      'telephone-input': 20,
      'text-input': 23,
      accordion: 14,
      modal: 11,
      rating: 18,
      password: 20,
         tnc: 12
       }],
   
       // Disable this rule for forms
       'xwalk/no-orphan-collapsible-fields': 'off'
     }
   }
   ```

**驗證：**&#x200B;確認 ESLint 可與表單元件搭配使用。

+++

+++步驟4：建置和部署

1. **安裝相依性並建置**

   ```bash
   # Install any new dependencies
   npm install
   
   # Build component definitions
   npm run build:json
   ```

   **其作用：**
   - 使用表單元件更新 `component-definition.json`
   - 使用表單模型產生 `component-models.json`
   - 使用篩選規則建立 `component-filters.json`

2. **驗證所產生的檔案**

   檢查專案根目錄中的這些檔案是否包含與表單相關的物件：
   - `component-definition.json`
   - `component-models.json`
   - `component-filters.json`

3. **認可並推送變更**

   ```bash
   git add .
   git commit -m "Add Adaptive Forms Block integration"
   git push origin main
   ```

**驗證：**&#x200B;確認您的專案包含表單功能。

+++

**下一步：**&#x200B;[建立第一份表單](#create-your-first-form)

## 建立第一份表單

**應該關注此節的人：**\
本節與路徑A （新專案）或路徑B （現有專案）之後的使用者相關。

現在您的專案已準備好建立表單，您可以使用通用編輯器的直覺式WYSIWYG製作環境來建置您的第一個表單。 下列步驟提供在AEM網站中設計、設定和發佈表單的結構化方法。

### 概觀

在「通用編輯器」中建立表單的過程包含幾個關鍵階段：

1. **插入最適化表單區塊**\
   首先，將最適化表單區塊新增至您選擇的頁面。

2. **新增表單元件**\
   插入文字欄位、按鈕和其他輸入元素等元件，填入您的表單。

3. **設定元件屬性**\
   調整每個元件的設定和屬性，以符合表單的需求。

4. **預覽和測試您的表單**\
   使用預覽功能在發佈之前驗證表單的外觀和行為。

5. **發佈更新的頁面**\
   在您滿意後，請發佈您的頁面，讓一般使用者也能使用表單。

以下幾節將詳細引導您完成這些步驟，以確保流暢而有效的表單建立體驗。

+++步驟1：新增最適化表單區塊

1. **在通用編輯器中開啟頁面**
   - 導覽至 AEM 中的 **Sites** 控制台
   - 選取要新增表單的頁面 (例如 `index`)
   - 按一下「**編輯**」

   您的頁面在通用編輯器中開啟，以進行 WYSIWYG 編輯。

2. **新增自適應表單元件**
   - 開啟&#x200B;**內容樹**&#x200B;面板 (左側邊欄)
   - 導覽到您想要新增表單的區段
   - 按一下「**新增**」(+) 圖示
   - 從元件清單中選取&#x200B;**自適應表單**

   ![新增自適應表單區塊](/help/edge/docs/forms/assets/add-adaptive-form-block.png)
   *圖：將自適應表單區塊新增至頁面*

**驗證：**&#x200B;確認您有一個空的表單容器。

+++

+++步驟2：新增表單元件

1. **導覽到您的表單區塊**
   - 在內容樹中尋找您最近新增的自適應表單區段

   ![已新增自適應表單區塊](/help/edge/docs/forms/assets/adative-form-block.png)
   *圖：內容樹中的自適應表單區塊*

2. **新增表單元件**

   您可以用兩種方式新增元件：

   **方法 A：按一下來新增**
   - 按一下表單區段中的「**新增**」(+) 圖示
   - 在&#x200B;**自適應表單元件**&#x200B;清單中選取元件

   **方法 B：拖放**
   - 將元件直接從元件面板拖曳到表單中

   ![新增表單元件](/help/edge/docs/forms/assets/add-component.png)
   *圖：新增元件至表單中*

   **建議的啟動元件：**
   - 文字輸入 (姓名、電子郵件)
   - 文字區域 (用於訊息)
   - 提交按鈕

3. **設定元件屬性**
   - 選取任何表單元件
   - 使用&#x200B;**屬性** 面板 (右側邊欄) 進行設定：
      - 標籤和預留位置
      - 驗證規則
      - 必填欄位設定

   ![元件屬性面板](/help/edge/docs/forms/assets/component-properties.png)
   *圖：設定元件屬性*

4. **預覽您的表單**

   您的表單大概是下面這個樣子：

   ![已完成的表單預覽](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *圖：使用通用編輯器建立的範例表單*

**驗證：**&#x200B;確認您的表單已準備好發佈。

>[!IMPORTANT]
>
> 請記住在進行變更後發佈您的頁面，才能在瀏覽器中看見更新。

+++

+++步驟3：發佈表單

1. **從通用編輯器發佈**
   - 在通用編輯器中按一下「**發佈**」按鈕

   ![發佈表單](/help/edge/docs/forms/assets/publish-form.png)
   *圖：從通用編輯器發佈表單*

2. **確認發佈**
   - 在確認對話框中，按一下「**發佈**」

   ![發佈確認](/help/edge/docs/forms/assets/publish-form1.png)
   *圖：確認發佈動作*

   您將看到確認出版的成功訊息。

   ![發佈成功](/help/edge/docs/forms/assets/publish-form2.png)
   *圖：出版成功確認*

3. **檢視您的上線表單**

   您的表單現已上線，網址：

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **範例 URL：**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

   ![上線表單頁面](/help/edge/docs/forms/assets/publish-index-page.png)
   *圖：您在 Edge Delivery Services 上發佈的表單頁面*

**恭喜！**&#x200B;您的表單現已上線並準備收集提交內容。

+++

### 後續步驟

現在您已經有可使用的表單，您可以：

- 透過編輯 CSS 和 JavaScript 檔案&#x200B;**自訂樣式**
- **新增進階表單功能**，例如驗證規則和條件式邏輯
- **設定本機開發**&#x200B;以便加速疊代
- 針對特定使用案例&#x200B;**建立獨立表單**

>[!TIP]
>
> **了解更多：**&#x200B;[在通用編輯器中建立獨立表單](/help/edge/docs/forms/universal-editor/create-forms.md)

## 設定本機開發環境

**最適合：**&#x200B;想要自訂表單樣式和行為的開發人員

在本機開發環境中，您可以進行變更並立即查看，無需經過發佈週期。

+++設定AEM CLI和本機開發

1. **安裝 AEM CLI**

   AEM CLI 簡化本機開發任務：

   ```bash
       npm install -g @adobe/aem-cli
   ```

2. **原地複製您的存放庫**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   使用您實際的 GitHub 詳細資訊取代 `<owner>` 和 `<repo>`。

3. **啟動本機開發伺服器**

   ```bash
   aem up
   ```

   這樣會啟動具有熱重新載入功能的本機伺服器。

4. **進行自訂**

   - 編輯 `blocks/form/` 目錄裡的檔案以修改表單樣式和行為
   - 修改 `form.css` 以自訂樣式
   - 更新 `form.js` 來自訂行為

   在您的瀏覽器中&#x200B;**立即查看變更**，網址：`http://localhost:3000`

5. **部署您的變更**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   您可以透過以下位置檢視變更：
   - **預覽：**`https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **生產：**`https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## 疑難排解

### 常見問題和解決方案

+++GitHub建置問題

**問題：**&#x200B;建置失敗或 linting 錯誤

**解決方案 1：處理 Linting 錯誤**

如果遇到 linting 錯誤：

1. 在專案根目錄中開啟 `package.json`
2. 找到 `lint` 指令碼：

   ```json
   "scripts": {
     "lint": "npm run lint:js && npm run lint:css"
   }
   ```

3. 暫時停用 linting：

   ```json
   "scripts": {
     "lint": "echo 'skipping linting for now'"
   }
   ```

4. 認可並推送變更

**解決方案 2：模組路徑錯誤**

如果您看到「無法解析模組『/scripts/lib-franklin.js』的路徑」：

1. 導覽至 `blocks/form/form.js`
2. 更新匯入語句：

   ```javascript
   // Change this:
   import { ... } from '/scripts/lib-franklin.js';
   
   // To this:
   import { ... } from '/scripts/aem.js';
   ```

+++

+++表單功能問題

**問題：**&#x200B;表單提交無法運作

**解決方案：**

- 確認您有一個提交按鈕元件
- 檢查表單動作 URL 設定
- 確認表單驗證規則
- 先在預覽模式下測試

**問題：**&#x200B;樣式問題

**解決方案：**

- 檢查 `blocks/form/` 中的 CSS 檔案路徑
- 清除瀏覽器快取
- 驗證 CSS 語法
- 在本機開發環境中測試

+++

+++通用編輯器問題

**問題：**&#x200B;表單元件未出現在通用編輯器中

**解決方案：**

- 確認 AEM Code Sync 是否已安裝並正在執行
- 檢查 `fstab.yaml` 具有正確的 AEM 作者 URL
- 確保您的 AEM 實例已啟用搶先體驗功能
- 確認 `component-definition.json` 包括表單元件

**問題：**&#x200B;發佈後看不見變更

**解決方案：**

- 等待內容傳遞網路快取重新整理
- 檢查瀏覽器快取 (嘗試無痕視窗/私人模式)
- 確認是否使用正確的 URL 格式

+++



