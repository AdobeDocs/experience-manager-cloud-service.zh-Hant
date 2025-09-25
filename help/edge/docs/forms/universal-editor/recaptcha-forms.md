---
title: 在通用編輯器中將 Google reCAPTCHA 新增到表單
description: 在 Edge Delivery Services 表單中實施 Google reCAPTCHA 保護來防止垃圾郵件和自動化攻擊的指南
feature: Edge Delivery Services
keywords: 表單中的 reCAPTCHA, 在通用編輯器中使用 reCAPTCHA, 在表單中新增 reCAPTCHA, 表單安全性, 垃圾郵件防護
role: Developer, Admin
level: Intermediate
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: ht
source-wordcount: '1281'
ht-degree: 100%

---


# 在通用編輯器中將 Google reCAPTCHA 新增到表單

Google reCAPTCHA 會區分人類使用者和自動機器人，能夠協助保護表單安全。本指南介紹如何在通用編輯器中實施 reCAPTCHA 企業版和標準版。

**目標：**

- 選取合適的 reCAPTCHA 解決方案
- 設定 reCAPTCHA 企業版或標準版
- 將 reCAPTCHA 新增至您的表單
- 驗證並測試實施情況
- 監控和最佳化效能

## 先決條件

在開始之前，請確保您已具備以下條件：

### 存取要求

- AEM as a Cloud Service 製作存取權
- 具有表單編輯權限的通用編輯器存取權

### 技術要求

- 有效的 Google 帳戶
- 企業版：已啟用計費的 Google Cloud Platform 專案
- 標準版：Google reCAPTCHA 帳戶
- 已驗證表單的網域名稱所有權

### 知識要求

- 對 AEM Forms 和通用編輯器有基本的了解
- 熟悉雲端服務設定
- 理解表單安全性概念

## 為什麼要在表單中使用 reCAPTCHA？

| ![安全性](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![機器人防護](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![使用者體驗](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **增強安全性** | **機器人與垃圾郵件預防** | **順暢的使用者體驗** |
| 保護表單免於受到詐騙活動和攻擊的傷害 | 防止自動機器人提交表單 | 隱形 reCAPTCHA 不會干擾合法使用者 |

**關鍵概念：** reCAPTCHA 使用機器學習來分析使用者行為並指派一個分數 (0.0 到 1.0) 來表示人機互動的可能性。分數越高表示是人類使用者；分數越低表示是機器人。

**範例：**&#x200B;處理敏感資料的稅務計算表單需要防範自動化攻擊的保護。reCAPTCHA 驗證提交的內容來自真實使用者，而不是機器人。

## 選擇 reCAPTCHA 解決方案

Edge Delivery Services 表單支援兩種 Google reCAPTCHA 選項。使用以下準則來選取正確的解決方案：

### 快速決策指南

**如果您有以下情況，請使用 reCAPTCHA 企業版：**

- 高流量表單 (每月超過 10,000 個請求)
- 嚴格的合規性要求 (GDPR、SOX、HIPAA)
- 需要進階分析和報告
- 購買進階安全性功能的預算
- 複雜的多網域部署

**如果您有以下情況，請使用 reCAPTCHA 標準版：**

- 低到中等流量 (每月小於 10,000 個請求)
- 基本安全性需求
- 預算有限 (免費層級)
- 簡單的單網域設定
- 不熟悉 reCAPTCHA

### 詳細比較

| **功能** | **reCAPTCHA Enterprise** | **reCAPTCHA Standard** |
|-------------|--------------------------|------------------------|
| **成本** | 付費 (根據使用情況定價) | 免費 |
| **請求限制** | 無限制 | 每月 100 萬個請求 |
| **進階分析** | 詳細報告 | 僅基本統計數據 |
| **自訂規則** | 帳戶特定規則 | 僅全域規則 |
| **支援多網域** | 進階管理 | 基本支援 |
| **SLA** | 保證 99.9% 正常運作時間 | 盡合理努力 |
| **支援** | 企業支援 | 社群支援 |
| **合規性** | 企業級 | 標準合規性 |

**兩種解決方案均提供：**

- 分數型偵測 (分級 0.0 到 1.0)
- 隱形操作 (無需與使用者互動)
- 機器學習驅動的機器人偵測
- 即時風險評估

## 設定 reCAPTCHA 企業版


+++ 步驟 1：準備 Google Cloud 環境

**要求：**

1. 已啟用計費的 Google Cloud 專案
2. 專案 ID (來自 GCP 儀表板)
3. 表單的網域驗證
4. 管理員對 GCP 和 AEM 的存取權

**設定：**

1. 建立或選取 Google Cloud 專案
   - 前往 [Google Cloud Console](https://console.cloud.google.com/)
   - 建立新專案或選取現有專案
   - 記下您的專案 ID

2. 啟用 reCAPTCHA 企業版 API
   - 前往「API 和服務」>「資料庫」
   - 搜尋「reCAPTCHA 企業版 API」
   - 按一下「啟用」

3. 建立 API 認證
   - 前往「API 和服務」>「認證」
   - 按一下「建立認證」>「API 金鑰」
   - 複製並儲存您的 API 金鑰

4. 建立網站金鑰
   - 前往「安全性」>「reCAPTCHA 企業版」
   - 按一下「建立金鑰」
   - 選擇分數型金鑰類型
   - 新增您的網域
   - 設定臨界值分數 (建議：0.5)

**驗證查核點：**&#x200B;確保您已有：

- 專案 ID
- API 金鑰
- 網站金鑰
- 在 Google Cloud 中已驗證的網域

+++

+++ 步驟 2：設定 AEM 雲端設定容器

![逐步進行雲端設定](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)
*圖：為表單容器啟用雲端設定*

**設定：**

1. 存取設定瀏覽器
   - 登入您的 AEM 作者實例
   - 前往「工具」>「一般」>「設定瀏覽器」。

2. 啟用雲端設定
   - 找到表單的設定容器
   - 選取屬性
   - 檢查雲端設定
   - 按一下「儲存並關閉」。

3. 檢查設定
   - 確認容器屬性中出現「雲端設定」

**驗證查核點：**

- 為您的容器啟用雲端設定
- 容器出現在設定瀏覽器中
- 屬性顯示「雲端設定」已啟用

+++

+++ 步驟 3：在 AEM 中設定 reCAPTCHA 企業服務

![reCAPTCHA 企業版設定螢幕](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)
*圖：AEM 中的 reCAPTCHA 企業版設定介面*

**設定：**

1. 存取 reCAPTCHA 設定
   - 前往「工具」>「雲端服務」>「reCAPTCHA」
   - 選取表單的設定容器
   - 按一下「建立」

2. 進行企業設定
   - 標題：說明性名稱 (例如「生產 reCAPTCHA」)
   - 名稱：系統名稱 (自動產生或自訂)
   - 版本：選取 ReCAPTCHA 企業版
   - 專案 ID：輸入您的 Google Cloud 專案 ID
   - 網站金鑰：輸入來自 Google Cloud 的網站金鑰
   - API 金鑰：輸入您的 Google Cloud API 金鑰
   - 金鑰類型：選取分數型網站金鑰

3. 設定安全性臨界值
   - 臨界值分數：設定在 0.0 到 1.0 之間
   - 建議值：
      - 0.7-0.9：高安全性 (可能會阻止一些合法使用者)
      - 0.5-0.7：平衡安全性 (建議)
      - 0.1-0.5：較低安全性 (允許更多使用者)

4. 儲存並發佈
   - 按一下「建立」以儲存設定
   - 按一下「發佈」以便開放使用

**驗證查核點：**

- 設定已成功儲存
- 已完成所有必填欄位
- 設定已發佈且可見
- 無錯誤訊息

+++

## 設定 reCAPTCHA 標準版

+++步驟 1：取得 reCAPTCHA API 金鑰 (請參閱詳細資訊)

>[!IMPORTANT]
>
> Edge Delivery Services 表單僅支援 reCAPTCHA v2 (分數型)。不要使用核取方塊版本。

**金鑰產生：**

1. 存取 Google reCAPTCHA 控制台

   - 前往 [Google reCAPTCHA 管理控制台](https://www.google.com/recaptcha/admin)
   - 使用您的 Google 帳戶登入

2. 建立新網站

   - 按一下「+」新增網站
   - 標籤：輸入說明性名稱
   - reCAPTCHA 類型：選取 reCAPTCHA v2 >「我不是機器人」隱形
   - 網域：新增您的表單網域
   - 接受條款並按一下「提交」

3. 收集金鑰

   - 網站金鑰：複製網站金鑰 (公開金鑰)
   - 秘密金鑰：複製秘密金鑰 (私密金鑰)

**驗證查核點：**

- 在 reCAPTCHA 控制台中建立的網站

- 已取得網站金鑰

- 已取得秘密金鑰

- 已新增並驗證網域

+++

+++步驟 2：設定 AEM 雲端設定容器 (請參閱詳細資訊)

依照與企業版設定相同的流程：

1. 在設定瀏覽器中啟用雲端設定

2. 驗證容器設定

3. 確認設定已儲存

+++

+++步驟 3：在 AEM 中設定 reCAPTCHA 標準版服務 (請參閱詳細資訊)

![reCAPTCHA 標準版設定螢幕畫面](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)
*圖：AEM 中的 reCAPTCHA 標準版設定介面*

**設定：**

1. 存取 reCAPTCHA 設定

   - 前往「工具」>「雲端服務」>「reCAPTCHA」
   - 選取表單的設定容器
   - 按一下「建立」

2. 進行標準版設定

   - 標題：說明性名稱 (例如「標準版 reCAPTCHA」)
   - 名稱：系統名稱 (自動產生或自訂)
   - 版本：選取 ReCAPTCHA v2 版本
   - 網站金鑰：輸入您的 Google reCAPTCHA 網站金鑰
   - 秘密金鑰：輸入您的 Google reCAPTCHA 秘密金鑰

3. 儲存並發佈

   - 按一下「建立」以儲存設定
   - 按一下「發佈」以便開放使用

**驗證查核點：**

- 建立的設定無錯誤

- 兩個金鑰均輸入正確

- 設定已成功發佈

- 設定出現在清單中

+++

## 將 reCAPTCHA 新增至您的表單

設定 reCAPTCHA 服務後，請按照以下方式為表單新增保護：

![將 reCAPTCHA 元件加入表單](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)
*圖：將隱形驗證碼元件加入表單*

+++&#x200B;1. 在通用編輯器中開啟表單
前往您在 AEM Sites 中的表單並按一下「編輯」，在通用編輯器中開啟表單。等待編輯器載入。

- 前往您在 AEM Sites 中的表單
- 按一下「編輯」以便在通用編輯器中開啟
- 等待編輯器載入
+++

+++&#x200B;2. 找到表單結構
在內容樹 (左側面板) 中，找到您的自適應表單區段並展開表單結構查看插入點。

- 在內容樹 (左側面板) 中，找到您的自適應表單區段
- 展開表單結構以查看插入點
+++

+++&#x200B;3. 新增 reCAPTCHA 元件
將驗證碼 (隱形) 元件新增至您的表單。

- 按一下表單區段中的「新增」(+) 圖示
- 從元件清單中，選取驗證碼 (隱形)
- 或者，從元件面板拖放元件
+++

+++&#x200B;4. 設定元件 (選用)
選取新增的驗證碼元件並驗證其是否使用您的 reCAPTCHA 設定。

- 選取新增的驗證碼元件
- 在「屬性」面板中，驗證其是否使用您的 reCAPTCHA 設定
- 基本設定不需要額外設定
+++

+++&#x200B;5. 發佈您的變更
發佈您的變更並驗證其沒有錯誤。

- 在通用編輯器中按一下「發佈」
- 等待確認
- 確認沒有出現錯誤
+++

### 確認實施

受保護的表單現在可從以下網址取得：

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/
<form-name>
```

**範例 URL：**

```
https://main--my-forms--company.aem.live/content/forms/af/
contact-us-form
```
