---
title: 使用Edge Delivery Services建立及發佈最適化Forms
description: 在AEM中使用核心元件或Forms範本來建立、編寫和發佈最適化Edge Delivery Services的逐步指示，著重於技術精確度和清晰度。
keywords: 調適型表單，邊緣交付服務，核心元件，通用編輯器，表單建立， AEM forms，範本選擇，表單發佈
feature: Edge Delivery Services
role: User, Developer
level: Beginner
exl-id: 1eab3a3d-5726-4ff8-90b9-947026c17e22
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 3%

---


# 使用Edge Delivery Services建立及發佈最適化Forms

本檔案提供使用Edge Delivery Services在AEM中建立、設定和發佈最適化Forms的說明。 內容涵蓋核心元件和Edge Delivery Services範本。

在本指南結束時，您將瞭解如何：

- 為您的使用案例選取適當的範本型別
- 使用核心元件或Edge Delivery Services範本建立表單
- 使用正確的編輯器編寫表單
- 設定表單並發佈至Edge Delivery Services
- 存取已發佈的表單並確認部署

## 範本選取

開始之前，請先決定符合您需求的範本型別：

| 條件 | 核心元件範本 | Edge Delivery Services範本 |
|-------------------------|-----------------------------------------|-------------------------------------|
| 最適合 | 企業工作流程，複雜的整合 | 高效能公用表單 |
| 編輯器 | 自適應表單編輯器 | 通用編輯器 |
| 發佈 | AEM發佈+ Edge Delivery Services | 僅限Edge Delivery Services |
| 複雜性 | 進階表單功能 | 簡化快速表單 |
| 整合 | 完整的AEM生態系統 | Git型開發 |
| 學習曲線 | AEM使用者熟悉 | 現代、簡化的方法 |

**決定指引：**

![範本選擇決定](/help/edge/docs/forms/universal-editor/assets/template-selection-decision.svg)

- 將&#x200B;**核心元件**&#x200B;用於複雜的工作流程、深入的AEM整合，或利用現有的AEM資產。
- 使用&#x200B;**Edge Delivery Services**&#x200B;以提升效能、簡化功能和最新的開發實務。


*選擇適當範本型別的決定流程圖*

## 先決條件

繼續之前，請先確認已符合下列必要條件：

### 技術需求

- **AEM Forms as a Cloud Service**：具有Forms授權的有效製作執行個體。
- **GitHub帳戶**：儲存庫管理的個人或組織帳戶。
- **存放庫設定**：選擇下列其中一項：
   - **新專案**： [建立具有最適化AEM區塊的新Forms專案](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)。 存放庫已針對Edge Delivery Services預先設定。
   - **現有專案**： [將最適化Forms區塊新增至現有存放庫](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)並更新設定。

### 環境設定

- **AEM-GitHub連線**： [在您的AEM執行個體和GitHub存放庫之間建立連線](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)。
- **Edge Delivery Services**：確定存放庫已設定為自動部署。
- **許可權**：確認您擁有建立及發佈表單所需的存取許可權。

### 設定驗證


1. 確認GitHub存放庫包含最適化Forms區塊。
2. 測試AEM與您的GitHub存放庫之間的連線。
3. 確定您可以將內容發佈至Edge Delivery Services。



## 表單建立與發佈工作流程

此程式包含三個主要階段：

- **階段1：** [範本選取與表單建立](#step-1-template-selection-and-form-creation)
- **階段2：** [表單撰寫與設計](#step-2-form-authoring-and-design)
- **階段3：** [設定和發佈](#step-3-configuration-and-publishing)

每個階段都包含驗證步驟，以確認正確的設定。

![三階段工作流程](/help/edge/docs/forms/universal-editor/assets/three-phase-workflow.svg)
*表單建立與發佈的三個主要階段概述*

### 步驟1：範本選取和表單建立

根據您的範本選擇選取工作流程：

>[!BEGINTABS]

>[!TAB Edge Delivery Services範本]

**使用案例：**&#x200B;高效能表單與現代開發工作流程。

**功能：** Universal Editor編寫和Edge Delivery Services發佈。

#### 程式

1. **存取表單建立**
   - 登入您的AEM Forms as a Cloud Service作者例項。
   - 導覽至&#x200B;**Adobe Experience Manager** > **Forms** > **Forms與檔案**。
   - 按一下&#x200B;**建立** > **最適化Forms**。

1. **選取範本**
   - 在&#x200B;**Source**&#x200B;索引標籤中，選取&#x200B;**Edge Delivery Services範本**。
   - **建立**&#x200B;按鈕變為啟用。

     ![建立 EDS 表單](/help/edge/assets/create-eds-forms.png)

1. **設定選項（選擇性）**
   - **資料Source索引標籤**：視需要選取資料整合。
   - **提交標籤**：選擇提交動作（稍後可以設定）。
   - **傳遞標籤**：設定發佈/取消發佈排程。

1. **完成表單設定**
   - 按一下&#x200B;**建立**&#x200B;以開啟表單建立精靈。
   - 輸入下列內容：
      - **名稱**：內部識別碼（無空格，使用連字型大小）。
      - **標題**：顯示表單的名稱。
      - **GitHub URL**：存放庫URL （例如`https://github.com/your-org/your-repo`）。

   ![建立表單精靈](/help/edge/assets/create-form-wizard.png)

1. **驗證**
   - 按一下&#x200B;**建立**&#x200B;之後，請驗證：
      - 表單會在通用編輯器中開啟。
      - GitHub URL已正確連結。
      - 元件浮動視窗可供使用。
      - 表單畫布可見。

   ![通用編輯器介面](/help/edge/assets/author-form.png)

**結果：**&#x200B;表單已準備好在Universal Editor中編寫。

>[!TAB 核心元件範本]

**使用案例：**&#x200B;企業工作流程與複雜整合。

**功能：**&#x200B;最適化Forms編輯器編寫、雙重發佈(AEM + Edge Delivery Services)、進階表單功能。

#### 程式

1. **存取表單建立**
   - 登入您的AEM Forms as a Cloud Service作者例項。
   - 導覽至&#x200B;**Adobe Experience Manager** > **Forms** > **Forms與檔案**。
   - 按一下&#x200B;**建立** > **最適化Forms**。

1. **選取範本和佈景主題**
   - 在&#x200B;**Source**&#x200B;索引標籤中，選取&#x200B;**核心元件型範本**。
   - 選擇樣式的&#x200B;**佈景主題**。
   - **建立**&#x200B;按鈕變為啟用。

   ![核心元件範本選擇](/help/forms/assets/core-component-based-template.png)

1. **設定選項（選擇性）**
   - **資料Source索引標籤**：視需要選取資料整合。
   - **提交標籤**：選擇提交動作（稍後可以設定）。
   - **傳遞標籤**：設定發佈/取消發佈排程。

1. **完成表單設定**
   - 按一下&#x200B;**建立**&#x200B;以開啟表單建立精靈。
   - 輸入下列內容：
      - **名稱**：內部識別碼（無空格，使用連字型大小）。
      - **標題**：顯示表單的名稱。
      - **路徑**： AEM存放庫中的儲存位置。

     ![建立表單精靈](/help/forms/assets/create-cc-form.png)

1. **驗證**
   - 按一下&#x200B;**建立**&#x200B;之後，請驗證：
      - 表單會在最適化Forms編輯器中開啟。
      - 元件工具列可供使用。
      - 屬性面板可供存取。
      - 套用主題樣式。

     ![自適應表單編輯器](/help/forms/assets/af-editor-form.png)

**結果：**&#x200B;表單已準備好在最適化Forms編輯器中編寫。

>[!ENDTABS]

### 步驟2：表單製作與設計

製作體驗會依範本而異：

- **Edge Delivery Services範本**：通用編輯器
- **核心元件範本**：最適化Forms編輯器

![編輯器比較](/help/edge/docs/forms/universal-editor/assets/editor-comparison.svg)
*比較通用編輯器與最適化Forms編輯器功能*

>[!BEGINTABS]

>[!TAB 通用編輯器(Edge Delivery Services)]

**介面：**&#x200B;針對效能最佳化的現代化精簡編輯。

#### 新增表單元件

1. **存取元件庫**
   - 在通用編輯器中開啟內容瀏覽器。
   - 導覽至內容樹狀結構中的&#x200B;**最適化表單**&#x200B;元件。

   ![內容樹狀導覽](/help/edge/assets/content-tree.png)

1. **新增表單欄位**
   - 按一下&#x200B;**新增**&#x200B;圖示以開啟元件庫。
   - 從&#x200B;**最適化表單元件**&#x200B;清單中選取元件。
   - 將元件拖放至表單畫布上。

   ![新增元件](/help/edge/assets/add-component.png)

1. **設計表單**
   - 在屬性面板中設定欄位屬性。
   - 設定驗證規則和行為。
*s視需要調整樣式和版面。

   ![已完成登錄檔單](/help/edge/assets/contact-us.png)

#### 驗證

- 出現所有必填欄位。
- 欄位屬性已正確設定。
- 配置回應式且易於存取。
- 驗證規則會如預期運作。

#### 後續步驟

- [設定提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)以進行資料處理。
- 進階功能的[通用編輯器指南](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)。

>[!TAB 最適化Forms編輯器（核心元件）]

**介面：**&#x200B;完整的編輯功能，提供進階表單功能。

#### 新增表單元件

1. **存取元件庫**
   - 在「**將元件拖曳到這裡**」區段按一下「**插入元件**」。

   ![元件插入區域](/help/forms/assets/drag-components-af-editor.png)

2. **新增表單欄位**
   - 瀏覽&#x200B;**最適化表單元件**&#x200B;清單。
   - 將所需的元件拖曳至表單。
   - 使用進階元件，例如面板、精靈和資料整合。

   ![新增元件庫](/help/forms/assets/add-component-af.png)

3. **設計表單**
   - 在屬性面板中設定欄位屬性。
   - 設定複雜的驗證規則和商業邏輯。
   - 套用主題和進階樣式。

   ![已完成的登錄檔單](/help/forms/assets/af-editor-form.png)

#### 驗證

- 出現所有必填欄位。
- 已設定複雜的驗證規則。
- 套用主題樣式。
- 資料整合如預期運作（如適用）。

#### 後續步驟

- [設定進階工作流程的提交動作](/help/forms/configure-submit-actions-core-components.md)。
- 適用於企業功能的[核心元件指南](/help/forms/creating-adaptive-form-core-components.md)。

>[!ENDTABS]

### 步驟3：設定和發佈

設定Edge Delivery Services並發佈您的表單。 流程會依範本型別而有所不同。

#### Edge Delivery Services設定

>[!BEGINTABS]
>[!TAB Edge Delivery Services範本（自動）]

**組態：**&#x200B;自動（不需要手動設定）。

- GitHub存放庫連線和Edge Delivery Services設定是在表單建立期間建立。
- 發佈端點已自動設定。

**驗證：**

- 確認表單設定中顯示的設定。
- 請確定GitHub URL已正確連結。

![自動EDS組態](/help/edge/assets/aem-instance-eds-configuration.png)

>[!TAB 核心元件範本（手動）]

**組態：**&#x200B;需要手動設定。

#### 手動設定步驟

1. **存取組態工具**
   - 導覽至&#x200B;**工具** > **雲端服務** > **Edge Delivery Services設定**。

   ![EDS組態存取](/help/edge/assets/select-eds-conf.png)

1. **建立設定**
   - 選取符合表單名稱的資料夾（例如，`forms/enrollment-form`）。
   - 按一下&#x200B;**建立** > **組態**。

   ![建立EDS組態](/help/forms/assets/create-eds-conf.png)

1. **設定屬性**
   - 按一下&#x200B;**Edge Delivery Services設定**。
   - 選取&#x200B;**屬性**&#x200B;以開啟設定對話方塊。

   ![組態屬性](/help/forms/assets/eds-conf.png)

1. **設定引數**
   - **必要：**
      - **組織**： GitHub組織名稱。
      - **網站名稱**： GitHub存放庫名稱。
      - **分支**：分支名稱（主目錄留空）。
   - **選擇性：**
      - **Edge主機**：預設（同時發佈至.page和.live）。
      - **網站驗證Token**：為了安全驗證（如果需要）。

1. **儲存組態**
   - 按一下&#x200B;**儲存並關閉**。

#### 驗證

- 已成功建立設定。
- 已正確指定GitHub組織和存放庫。
- 分支設定與存放庫結構相符。
- 表單會出現在設定資料夾中。

>[!ENDTABS]

#### 發佈表單

>[!BEGINTABS]
>[!TAB 通用編輯器發佈]

Edge Delivery Services範本的&#x200B;**&#x200B;**

1. 在Universal Editor中，按一下&#x200B;**發佈**&#x200B;按鈕（右上角）。
2. 在對話方塊中確認發佈成功。
3. 請注意為階段版本和即時版本產生的URL。

   ![通用編輯器發佈](/help/edge/assets/publish-form.png)

- [發佈指南](/help/edge/docs/forms/universal-editor/publish-forms.md)

>[!TAB 最適化Forms編輯器發佈]

1. 在Experience Manager Forms主控台中，選取要發佈的表單。
2. 按一下工具列中的&#x200B;**[!UICONTROL 發佈]**。 檢閱要發佈的參考資產。

![在自適應表單編輯器上發佈表單](/help/forms/assets/publish-af-editor.png)

>[!NOTE]
>
> 如需詳細資訊，請參閱[在Experience Manager Forms中管理出版物](/help/forms/manage-publication.md)。

>[!ENDTABS]

## 表單URL

已發佈的表單可透過Edge Delivery Services URL存取。

### URL結構

- **階段（預覽/測試）：**

  ```
  https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>
  ```

- **即時（生產）：**

  ```
  https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
  ```

#### URL 參數

- `<branch>`： GitHub分支名稱（例如，`main`、`develop`）
- `<repo>`： GitHub存放庫名稱（例如，`my-forms-project`）
- `<owner>`： GitHub組織或使用者名稱（例如`company-name`）
- `<form_name>`：在AEM中定義的表單識別碼（例如，`contact-us`）

#### 範例

組織`contact-us`下儲存庫`forms-project`中表單`acme-corp`的範例：

- **已分段：** `https://main--forms-project--acme-corp.aem.page/content/forms/af/contact-us`
- **已上線：** `https://main--forms-project--acme-corp.aem.live/content/forms/af/contact-us`

#### 環境差異

- **分段(.page)：**&#x200B;測試的最新變更。
- **即時(.live)：**&#x200B;發佈的內容以供生產。

![URL結構](/help/edge/docs/forms/universal-editor/assets/url-structure.svg)
*Edge Delivery Services表單URL結構劃分*

#### 視覺範例

**Edge Delivery Services範本：**

- 已分段： ![登入表單已分段版本](/help/forms/assets/registration-form-staged-version.png)
- 已上線： ![登錄檔單已上線版本](/help/forms/assets/registration-form-live-version.png)

**核心元件範本：**

- 已分段： ![登錄檔單已分段版本](/help/forms/assets/enrollment-form-staged-version.png)
- 已上線： ![登錄檔單已上線版本](/help/forms/assets/enrollment-form-live-version.png)

## 疑難排解

以下是AEM Forms與Edge Delivery Services搭配使用的常見問題和解決方案。

+++表單未載入

**問題：**&#x200B;表單URL傳回404或空白頁面。

**解析度：**

- 從URL移除`.html`副檔名。
- 確認表單已發佈。
- 檢查GitHub存放庫中的最適化Forms區塊。
- 確保表單名稱與URL相符（區分大小寫）。

+++

+++設定問題

**問題：** Edge Delivery Services設定無法運作。

**解析度：**

- 請確定GitHub URL為`https://github.com/owner/repository`格式。
- 在設定中使用正確的分支名稱。
- 驗證存放庫存取權（公開或已驗證）。
- 檢查`fstab.yaml`以取得正確的GitHub詳細資料。

+++

+++發佈問題

**問題：**&#x200B;變更未出現在即時網站上。

**解析度：**

- 等待2至3分鐘，以進行CDN快取重新整理。
- 確認發佈工作流程已完成。
- 請先在分段(.page)環境中測試。
- 請確定GitHub存放庫已更新。

+++

+++通用編輯器問題

**問題：**&#x200B;無法編輯未載入的表單或元件。

**解析度：**

- 使用支援的瀏覽器(Chrome、Firefox、Safari)。
- 清除瀏覽器快取和Cookie。
- 驗證網路連線。
- 確認作者許可權。

+++

+++表單提交錯誤

**問題：**&#x200B;表單提交無法運作。

**解析度：**

- 在表單屬性中設定提交動作。
- 手動測試提交端點。
- 如果內嵌表單，請核取CORS設定。
- 驗證是否已設定必要欄位。

+++

+++效能問題

**問題：**&#x200B;載入表單速度緩慢或效能不佳。

**解析度：**

- 最佳化影像。
- 移除不必要的元件。
- 運用Edge Delivery Services CDN。
- 將自訂JavaScript/CSS最小化。

+++

+++取得協助

如果問題仍然存在：

1. 檢查Adobe Experience Cloud服務狀態。
2. 檢閱[Edge Delivery Services檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html)。
3. 造訪[Adobe Experience League社群](https://experienceleaguecommunities.adobe.com/)。
4. 聯絡Adobe客戶服務。

+++

## 後續步驟

完成表單建立和發佈後，請考量下列事項：

### 立即動作

- 使用本指南測試您的表單。
- 驗證您的GitHub存放庫和AEM連線。
- 檢閱範例表單。

### 進階主題

- [設定提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)：設定資料處理和整合。
- [表單資料模型](/help/forms/create-form-data-models.md)：將表單連線至後端資料來源。

### 效能最佳化

- [Edge Delivery Services最佳實務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/edge-delivery/overview.html)：發揮最大效能。
- [表單分析](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/analytics.html)：追蹤表單效能和使用者行為。

