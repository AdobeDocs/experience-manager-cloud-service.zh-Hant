---
title: 使用通用編輯器的AEM Forms適用的Edge Delivery Services快速入門
description: 瞭解如何使用Edge Delivery Services搭配Universal Editor的WYSIWYG撰寫功能來建立和發佈高效能表單。
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
exl-id: 24a23d98-1819-4d6b-b823-3f1ccb66dbd8
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '2609'
ht-degree: 1%

---


# 使用通用編輯器的AEM Forms適用的Edge Delivery Services快速入門

| 製作方法 | 指南 |
|---------------------------------|-----------------------------------------------------------------------|
| **通用編輯器 (WYSIWYG)** | 本文章 |
| **文件型編寫** | [以檔案為基礎的教學課程](/help/edge/docs/forms/tutorial.md) |

適用於AEM Forms的Edge Delivery Services結合高效能Web傳遞與Universal Editor中的WYSIWYG製作。 本指南涵蓋建立、自訂和發佈快速載入的表單。

## 您將會達成的目標

在本教學課程結束時，您將：

- 使用最適化Forms區塊設定GitHub存放庫
- 建立與Edge Delivery Services整合的AEM網站
- 使用通用編輯器建置和發佈表單
- 設定本機開發環境

## 選擇您的路徑

選取符合您情境的方法：

![選擇您的路徑決定指南](/help/edge/docs/forms/universal-editor/assets/choose-your-path.svg)
*圖：協助您選擇正確實作路徑的視覺化指南*

| **路徑A：新專案** | **路徑B：現有的專案** |
|----------------------------------------|-------------------------------------------|
| 從預先設定的範本開始 | 新增表單至您目前的AEM專案 |
| **最適合：**&#x200B;個新實作 | **最適合：**&#x200B;現有AEM Sites |
| **您的收藏：**&#x200B;預先設定的Forms區塊 | **您獲得的：** Forms已新增至現有網站 |
| **步驟：**&#x200B;設定Forms→範本→ | **步驟：**&#x200B;整合→設定→Forms |
| [以路徑A](#path-a-create-new-project-with-forms)開始 | [以路徑B](#path-b-add-forms-to-existing-project)開始 |

## 先決條件

為確保使用通用編輯器在AEM Forms中能順暢而成功地使用Edge Delivery Services，在繼續之前，請檢閱並確認下列必要條件：

### 存取需求

- **GitHub帳戶**：您必須擁有有權建立新存放庫的GitHub帳戶。 這對於管理您的專案原始程式碼以及與團隊合作至關重要。
- **AEM as a Cloud Service編寫存取權**：請確定您擁有AEM as a Cloud Service環境的作者層級存取權。 建立、編輯和發佈表單需要此存取權。

### 技術需求

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
> 不熟悉AEM？ 從[AEM Sites快速入門手冊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html)開始。

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

1. **存取AEM Forms範本**
   - 移至[https://github.com/adobe-rnd/aem-boilerplate-forms](https://github.com/adobe-rnd/aem-boilerplate-forms)

   ![AEM Forms樣板範本](/help/edge/docs/forms/assets/eds-form-boilerplate.png)
   *圖：具有預先設定的最適化Forms區塊的AEM Forms樣板存放庫*

2. **建立您的存放庫**
   - 按一下&#x200B;**使用此範本** > **建立新的存放庫**

   ![從範本建立存放庫](/help/edge/docs/forms/assets/use-eds-form-template.png)
   *圖：使用範本建立新的存放庫*

3. **設定存放庫設定**
   - **所有者**：選取您的GitHub帳戶或組織
   - **存放庫名稱**：選擇描述性名稱（例如，`my-forms-project`）
   - **可見度**：選取&#x200B;**公用** (建議用於Edge Delivery Services)
   - 按一下&#x200B;**建立存放庫**

   ![存放庫組態](/help/edge/docs/forms/assets/name-eds-repo.png)
   *圖：正在設定您的新存放庫公開可見度*

**驗證：**&#x200B;確認您擁有以AEM Forms Boilerplate範本為基礎的新GitHub存放庫。

+++

+++步驟2：安裝AEM程式碼同步

AEM程式碼同步會自動同步AEM製作環境與GitHub存放庫之間的內容變更。

1. **安裝GitHub應用程式**
   - 移至[https://github.com/apps/aem-code-sync/installations/new](https://github.com/apps/aem-code-sync/installations/new)

2. **設定存取許可權**
   - 選取&#x200B;**僅選取存放庫**
   - 選擇您新建立的存放庫
   - 按一下&#x200B;**儲存**

   ![AEM程式碼同步安裝](/help/edge/docs/forms/assets/aem-code-sync-up.png)
   *圖：正在安裝AEM程式碼同步，並具有存放庫特定的許可權*

**檢查點：** AEM程式碼同步現已安裝，而且可以存取您的存放庫。

+++

+++步驟3：設定AEM整合

`fstab.yaml`檔案會將您的GitHub存放庫連線至AEM製作環境，以進行內容同步。

1. **瀏覽至您的存放庫**
   - 前往您新建立的GitHub存放庫
   - 您應該會看到AEM Forms樣板檔案

2. **建立fstab.yaml檔案**
   - 按一下根目錄中的&#x200B;**新增檔案** > **建立新檔案**
   - 為檔案命名`fstab.yaml`

   ![正在建立fstab.yaml檔案](/help/edge/docs/forms/assets/open-fstab.png)
   *圖：正在建立fstab.yaml組態檔*

3. **新增您的AEM連線詳細資料**

   複製並貼上下列設定，取代預留位置：

   ```yaml
   mountpoints:
     /: https://<aem-author>/bin/franklin.delivery/<owner>/<repository>/main
   ```

   **取代：**
   - `<aem-author>`：您的AEM as a Cloud Service作者URL （例如，`author-p12345-e67890.adobeaemcloud.com`）
   - `<owner>`：您的GitHub使用者名稱或組織
   - `<repository>`：您的存放庫名稱

   **範例：**

   ```yaml
   mountpoints:
     /: https://author-p12345-e67890.adobeaemcloud.com/bin/franklin.delivery/mycompany/my-forms-project/main
   ```

   ![正在編輯fstab.yaml檔案](/help/edge/docs/forms/assets/edit-fstab-file.png)
   *圖：設定AEM整合的掛接點*

4. **認可組態**
   - 新增認可訊息：「新增AEM整合設定」
   - 按一下&#x200B;**認可新檔案**

   ![認可fstab變更](/help/edge/docs/forms/assets/commit-fstab-changes.png)
   *圖：認可fstab.yaml設定*

**驗證：**&#x200B;確認您的GitHub存放庫連線至AEM。

    >[！NOTE]
    >
    >發生建置問題？ 請參閱[疑難排解GitHub組建問題](#troubleshooting-github-build-issues)。

+++

+++步驟4：建立連線至您GitHub存放庫的AEM網站。

1. **存取AEM Sites主控台**
   - 登入您的AEM as a Cloud Service編寫執行個體
   - 瀏覽至&#x200B;**網站**

   ![AEM Sites主控台](/help/edge/assets/select-sites.png)
   *圖：存取AEM Sites主控台*

2. **開始建立網站**
   - 按一下&#x200B;**建立** > **從範本建立網站**

   ![建立網站選項](/help/edge/docs/forms/assets/create-sites.png)
   *圖：從範本*&#x200B;建立新網站

3. **選取Edge Delivery Services範本**
   - 選擇&#x200B;**Edge Delivery Services網站**&#x200B;範本
   - 按一下&#x200B;**下一步**

   ![網站範本選取專案](/help/edge/docs/forms/assets/select-site-template.png)
   *圖：選取Edge Delivery Services網站範本*

   >[!NOTE]
   >
   >**範本無法使用？**&#x200B;如果您沒有看到Edge Delivery Services範本：
   >
   >1. 按一下&#x200B;**匯入**&#x200B;以上傳範本
   >2. 從[GitHub版本](https://github.com/adobe-rnd/aem-boilerplate-xwalk/releases)下載範本

4. **設定您的網站**

   輸入下列資訊：

   | 欄位 | 值 | 範例 |
   |-----------------|-----------------------------|-----------------------------------------|
   | **網站標題** | 網站的描述性名稱 | 「我的Forms專案」 |
   | **網站名稱** | URL易記名稱 | &quot;my-forms-project&quot; |
   | **GitHub URL** | 您的存放庫URL | `https://github.com/mycompany/my-forms-project` |

   ![站台組態](/help/edge/docs/forms/assets/create-aem-site.png)
   *圖：使用GitHub整合設定您的新AEM網站*

5. **完成網站建立**
   - 檢閱您的設定
   - 按一下「**建立**」。

   ![確認網站建立](/help/edge/docs/forms/assets/click-ok-aem-site.png)
   *圖：確認網站建立*

   **成功！**&#x200B;您的AEM網站現已建立並連線至GitHub。

6. **在通用編輯器中開啟**
   - 在Sites主控台中，找出新網站
   - 選取`index`頁面
   - 按一下&#x200B;**編輯**

   ![在通用編輯器中編輯網站](/help/edge/docs/forms/assets/edit-site.png)
   *圖：正在開啟您的網站以進行編輯*

   Universal Editor會在新標籤中開啟，提供WYSIWYG編寫功能。

   ![通用編輯器介面](/help/edge/docs/forms/assets/site-in-universal-editor.png)
   *圖：您的網站已在Universal Editor中開啟，以供WYSIWYG編輯*

**驗證：**&#x200B;確認您的AEM網站已準備好進行表單編寫。

+++

+++步驟5：發佈您的網站

發佈功能可讓您在Edge Delivery Services上取得全域存取權。

1. **從網站主控台快速發佈**
   - 返回AEM Sites主控台
   - 選取您的網頁（或使用Ctrl+A選取全部）
   - 按一下&#x200B;**快速發佈**

   ![發佈AEM網站](/help/edge/docs/forms/assets/publish-sites.png)
   *圖：選取頁面以進行快速發佈*

2. **確認發佈**
   - 在確認對話方塊中，按一下&#x200B;**發佈**

   ![快速發佈對話方塊](/help/edge/docs/forms/assets/quick-publish.png)
   *圖：確認發佈動作*

   **替代方案：**&#x200B;您也可以使用發佈按鈕直接從Universal Editor發佈。

   ![從通用編輯器發佈](/help/edge/docs/forms/assets/qui.png)
   *圖：直接從通用編輯器發佈*

3. **存取您的即時網站**

   您的網站現在已上線：

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **URL結構說明：**
   - `<branch>`： GitHub分支（通常為`main`）
   - `<repo>`：您的存放庫名稱
   - `<owner>`：您的GitHub使用者名稱或組織
   - `<site-name>`：您的AEM網站名稱

   **範例：**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

**驗證：**&#x200B;確認您的網站已在Edge Delivery Services上線。

>[!TIP]
>
> **URL模式：**
>
> - **首頁：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/`
> - **其他頁面：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/<page-name>`

**下一步：** [建立您的第一個表單](#create-your-first-form)

+++

## 路徑B：將Forms新增至現有專案

**最適合：**&#x200B;具有Edge Delivery Services的現有AEM Sites

如果您已有使用Edge Delivery Services的AEM專案，您可以整合最適化Forms區塊以新增表單功能。

### 路徑B的必要條件

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

1. **瀏覽至您的本機專案**

   ```bash
   cd /path/to/your/aem-project
   ```

2. **從AEM Forms範本下載必要的檔案**

   從[AEM Forms樣板存放庫](https://github.com/adobe-rnd/aem-boilerplate-forms)複製這些檔案：

   | 來源 | 目的地 | 用途 |
   |------------------------------------------------------------------------|----------------------------|----------------------------|
   | [`blocks/form/`](https://github.com/adobe-rnd/aem-boilerplate-forms/tree/main/blocks/form) | `blocks/form/` | 核心表單功能 |
   | [`scripts/form-editor-support.js`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.js) | `scripts/form-editor-support.js` | 通用編輯器整合 |
   | [`scripts/form-editor-support.css`](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/form-editor-support.css) | `scripts/form-editor-support.css` | 編輯器樣式 |

3. **更新編輯器支援**
   - 將您的`/scripts/editor-support.js`檔案取代為AEM Forms樣板[中的](https://github.com/adobe-rnd/aem-boilerplate-forms/blob/main/scripts/editor-support.js)editor-support.js

**驗證：**&#x200B;確認表單區塊檔案位於您的專案中。

+++

+++步驟2：更新元件設定

1. **更新區段模型**

   開啟`/models/_section.json`並將表單元件新增至篩選器：

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

   **這會做什麼：**&#x200B;啟用通用編輯器元件選擇器中的表單元件。

**驗證：**&#x200B;確認表單元件出現在通用編輯器中。

+++

+++步驟3：設定ESLint （選用）

**為什麼這個步驟：**&#x200B;避免表單特定檔案的Linting錯誤，並設定正確的驗證規則。

1. **更新.eslingnore**

   將這些行新增至`/.eslintignore`：

   ```bash
   # Form block rule engine files
   blocks/form/rules/formula/*
   blocks/form/rules/model/*
   blocks/form/rules/functions.js
   scripts/editor-support.js
   scripts/editor-support-rte.js
   ```

2. **更新.eslintrc.js**

   將這些規則新增至`rules`中的`/.eslintrc.js`物件：

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

**驗證：**&#x200B;確認ESLint可搭配表單元件使用。

+++

+++步驟4：建置和部署

1. **安裝相依性和組建**

   ```bash
   # Install any new dependencies
   npm install
   
   # Build component definitions
   npm run build:json
   ```

   **此功能的功能：**
   - 使用表單元件更新`component-definition.json`
   - 使用表單模型產生`component-models.json`
   - 使用篩選規則建立`component-filters.json`

2. **驗證產生的檔案**

   檢查專案根目錄中的這些檔案是否包含表單相關物件：
   - `component-definition.json`
   - `component-models.json`
   - `component-filters.json`

3. **認可及推播變更**

   ```bash
   git add .
   git commit -m "Add Adaptive Forms Block integration"
   git push origin main
   ```

**驗證：**&#x200B;確認您的專案包含表單功能。

+++

**下一步：** [建立您的第一個表單](#create-your-first-form)

## 建立您的第一個表單

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

1. **在通用編輯器中開啟您的頁面**
   - 導覽至AEM中的&#x200B;**網站**&#x200B;主控台
   - 選取您要新增表單的頁面（例如，`index`）
   - 按一下&#x200B;**編輯**

   您的頁面會在Universal Editor中開啟，以便進行WYSIWYG編輯。

2. **新增最適化表單元件**
   - 開啟&#x200B;**內容樹狀結構**&#x200B;面板（左側邊欄）
   - 導覽至您要新增表單的區段
   - 按一下&#x200B;**新增** (+)圖示
   - 從元件清單中選取&#x200B;**最適化表單**

   ![正在新增最適化表單區塊](/help/edge/docs/forms/assets/add-adaptive-form-block.png)
   *圖：新增最適化表單區塊至您的頁面*

**驗證：**&#x200B;確認您有空白的表單容器。

+++

+++步驟2：新增表單元件

1. **瀏覽至您的表單區塊**
   - 在內容樹狀結構中，找出您新增的最適化表單區段

   ![已新增最適化表單區塊](/help/edge/docs/forms/assets/adative-form-block.png)
   *圖：內容樹狀結構中的最適化表單區塊*

2. **新增表單元件**

   新增元件有兩種方式：

   **方法A：按一下以新增**
   - 按一下表單區段中的&#x200B;**新增** (+)圖示
   - 從&#x200B;**最適化表單元件**&#x200B;清單中選取元件

   **方法B：拖放**
   - 將元件直接從元件面板拖曳至您的表單

   ![正在新增表單元件](/help/edge/docs/forms/assets/add-component.png)
   *圖：正在新增元件至您的表單*

   **建議的起始元件：**
   - 文字輸入（針對名稱、電子郵件）
   - 文字區域（適用於訊息）
   - 提交按鈕

3. **設定元件屬性**
   - 選取任何表單元件
   - 使用&#x200B;**屬性**&#x200B;面板（右側邊欄）來設定：
      - 標籤和預留位置
      - 驗證規則
      - 必填欄位設定

   ![元件屬性面板](/help/edge/docs/forms/assets/component-properties.png)
   *圖：正在設定元件屬性*

4. **預覽您的表單**

   您的表單看起來會像這樣：

   ![完成的表單預覽](/help/edge/docs/forms/assets/added-form-aem-sites.png)
   *圖：使用通用編輯器建立的範例表單*

**驗證：**&#x200B;確認您的表單已準備好發佈。

>[!IMPORTANT]
>
> 進行變更後，請記得發佈您的頁面，以在瀏覽器中檢視更新。

+++

+++步驟3：發佈表單

1. **從通用編輯器發佈**
   - 按一下通用編輯器中的&#x200B;**發佈**&#x200B;按鈕

   ![正在發佈表單](/help/edge/docs/forms/assets/publish-form.png)
   *圖：從通用編輯器發佈您的表單*

2. **確認發佈**
   - 在確認對話方塊中，按一下&#x200B;**發佈**

   ![發佈確認](/help/edge/docs/forms/assets/publish-form1.png)
   *圖：確認發佈動作*

   您將看到確認發佈的成功訊息。

   ![發佈成功](/help/edge/docs/forms/assets/publish-form2.png)
   *圖：成功發行確認*

3. **檢視您的即時表單**

   您的表單現在已上線：

   ```
   https://<branch>--<repo>--<owner>.aem.page/content/<site-name>/
   ```

   **範例URL：**

   ```
   https://main--my-forms-project--mycompany.aem.page/content/my-forms-project/
   ```

   ![即時表單頁面](/help/edge/docs/forms/assets/publish-index-page.png)
   *圖：您在Edge Delivery Services上發佈的表單頁面*

**恭喜！**&#x200B;您的表單現在已上線並準備好收集提交內容。

+++

### 後續步驟

現在您有了工作表單，您可以：

- **編輯CSS和JavaScript檔案以自訂樣式**
- **新增進階表單功能**，例如驗證規則和條件式邏輯
- **設定本機開發**&#x200B;以加快反複專案
- **針對特定使用案例建立獨立表格**

>[!TIP]
>
> **深入瞭解：** [在通用編輯器中建立獨立表單](/help/edge/docs/forms/universal-editor/create-forms.md)

## 設定本機開發環境

**最適合：**&#x200B;想要自訂表單樣式和行為的開發人員

本機開發環境可讓您進行變更並立即檢視，而不需經過發佈週期。

+++設定AEM CLI和本機開發

1. **安裝AEM CLI**

   AEM CLI可簡化本機開發工作：

   ```bash
       npm install -g @adobe/aem-cli
   ```

2. **複製您的存放庫**

   ```bash
   git clone https://github.com/<owner>/<repo>
   cd <repo>
   ```

   將`<owner>`和`<repo>`取代為您實際的GitHub詳細資料。

3. **啟動本機開發伺服器**

   ```bash
   aem up
   ```

   這會啟動具有熱過載功能的本機伺服器。

4. **進行自訂**

   - 編輯`blocks/form/`目錄中的檔案以取得表單樣式和行為
   - 修改樣式的`form.css`
   - 更新`form.js`的行為

   **立即在瀏覽器中檢視變更** `http://localhost:3000`

5. **部署您的變更**

   ```bash
   git add .
   git commit -m "Custom form styling"
   git push origin main
   ```

   您的變更將可在以下網址取得：
   - **預覽：** `https://<branch>--<repo>--<owner>.aem.page/content/<site-name>`
   - **生產：** `https://<branch>--<repo>--<owner>.aem.live/content/<site-name>`

+++


## 疑難排解

### 常見問題和解決方案

+++GitHub建置問題

**問題：**&#x200B;組建失敗或Linting錯誤

**解決方案1：處理Linting錯誤**

如果您遇到線性錯誤：

1. 在您的專案根目錄中開啟`package.json`
2. 尋找`lint`指令碼：

   ```json
   "scripts": {
     "lint": "npm run lint:js && npm run lint:css"
   }
   ```

3. 暫時停用Linting：

   ```json
   "scripts": {
     "lint": "echo 'skipping linting for now'"
   }
   ```

4. 認可並推送變更

**解決方案2：模組路徑錯誤**

如果您看到「無法解析模組&#39;/scripts/lib-franklin.js&#39;的路徑」：

1. 瀏覽至`blocks/form/form.js`
2. 更新匯入陳述式：

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

- 確定您有提交按鈕元件
- 檢查表單動作URL設定
- 驗證表單驗證規則
- 先在預覽模式下測試

**問題：**&#x200B;樣式問題

**解決方案：**

- 檢查`blocks/form/`中的CSS檔案路徑
- 清除瀏覽器快取
- 驗證CSS語法
- 在本機開發環境中測試

+++

+++通用編輯器問題

**問題：**&#x200B;表單元件未出現在通用編輯器中

**解決方案：**

- 確認已安裝並執行AEM程式碼同步
- 檢查`fstab.yaml`是否有正確的AEM作者URL
- 確保您的AEM執行個體已啟用搶先存取
- 確認`component-definition.json`包含表單元件

**問題：**&#x200B;發佈後未顯示變更

**解決方案：**

- 等待CDN快取重新整理
- 檢查瀏覽器快取（嘗試無痕模式/私密模式）
- 確認使用正確的URL格式

+++



