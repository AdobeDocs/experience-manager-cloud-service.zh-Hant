---
title: 在通用編輯器中將Google reCAPTCHA新增至Forms
description: 在Edge Delivery Services表單中實作Google reCAPTCHA保護，以防止垃圾郵件和自動攻擊的指南
feature: Edge Delivery Services
keywords: 表單中的 reCAPTCHA、在通用編輯器中使用 reCAPTCHA、在表單中新增 reCAPTCHA、表單安全性、垃圾郵件防護
role: Developer, Admin
level: Intermediate
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 4%

---


# 在通用編輯器中將Google reCAPTCHA新增至Forms

Google reCAPTCHA可區分人類使用者和自動化機器人，有助於保護表單。 本指南說明如何在通用編輯器中實作reCAPTCHA Enterprise和Standard版本。

**目標：**

- 選取適當的reCAPTCHA解決方案
- 設定reCAPTCHA Enterprise或Standard
- 將reCAPTCHA新增至您的表單
- 驗證及測試實作
- 監控並最佳化效能

## 先決條件

開始之前，請確定您具備下列條件：

### 存取需求

- AEM as a Cloud Service製作存取權
- 具有表單編輯許可權的通用編輯器存取
- 註冊reCAPTCHA功能的搶先存取方案

### 技術需求

- 有效的Google帳戶
- 企業：已啟用計費的Google Cloud Platform專案
- 針對標準： Google reCAPTCHA帳戶
- 已驗證您表單的網域擁有權

### 知識需求

- 對AEM Forms和通用編輯器的基本瞭解
- 熟悉雲端服務設定
- 瞭解表單安全性概念

## 為何要在您的Forms中使用reCAPTCHA？

| ![安全性](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![機器人防護](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![使用者體驗](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **增強安全性** | **機器人與垃圾郵件預防** | **順暢的使用者體驗** |
| 保護表單免受詐騙活動和攻擊 | 防止自動機器人提交表單 | 不可見的reCAPTCHA不會破壞合法使用者 |

**金鑰概念：** reCAPTCHA使用機器學習來分析使用者行為，並指派分數（0.0到1.0）來表示人類互動的可能性。 分數越高表示人類使用者，分數越低表示機器人。

**範例：**&#x200B;處理敏感資料的稅捐計算表單需要自動攻擊的保護。 reCAPTCHA會驗證提交內容是否來自真正的使用者，而非機器人。

## 選擇 reCAPTCHA 解決方案

Edge Delivery Services Forms支援兩個Google reCAPTCHA選項。 使用下列條件來選取正確的解決方案：

### 快速決策指南

**如果您有：**，請使用reCAPTCHA Enterprise

- 高流量表單（每月>10,000個請求）
- 嚴格的法規遵循要求(GDPR、SOX、HIPAA)
- 需要進階分析和報告
- 高階安全性功能的預算
- 複雜的多網域部署

**如果您有：**，請使用reCAPTCHA Standard

- 低至中度流量（&lt;10,000個請求/月）
- 基本安全性需求
- 預算有限（免費套餐）
- 簡單的單一網域設定
- 是reCAPTCHA的新手

### 詳細比較

| **功能** | **reCAPTCHA Enterprise** | **reCAPTCHA Standard** |
|-------------|--------------------------|------------------------|
| **成本** | 付費（根據使用量定價） | 免費 |
| **要求限制** | 無限制 | 每月100萬項請求 |
| **進階分析** | 詳細報告 | 僅限基本統計資料 |
| **自訂規則** | 帳戶特定規則 | 僅限全域規則 |
| **多重網域支援** | 進階管理 | 基本支援 |
| **SLA** | 99.9%的連續運作時間保證 | 盡力而為 |
| **支援** | 企業支援 | 社群支援 |
| **法規遵循** | 企業級 | 標準合規性 |

**兩個解決方案都提供：**

- 以分數為基礎的偵測（0.0至1.0縮放）
- 隱藏的作業（不需要使用者互動）
- 機器學習支援的機器人偵測
- 即時風險評估

## 設定 reCAPTCHA Enterprise


+++ 步驟1：準備Google雲端環境

**需求：**

1. 已啟用計費的Google雲端專案
2. 專案ID （從GCP儀表板）
3. 您的表單的網域驗證
4. GCP和AEM的管理員存取權

**安裝程式：**

1. 建立或選取Google Cloud專案
   - 移至[Google Cloud Console](https://console.cloud.google.com/)
   - 建立新專案或選取現有專案
   - 記下您的專案ID

2. 啟用reCAPTCHA Enterprise API
   - 前往「API與服務>資料庫」
   - 搜尋「reCAPTCHA Enterprise API」
   - 按一下啟用

3. 建立API認證
   - 前往「API與服務>認證」
   - 按一下「建立認證> API金鑰」
   - 複製並儲存您的API金鑰

4. 建立網站金鑰
   - 前往安全性> reCAPTCHA Enterprise
   - 按一下「建立金鑰」
   - 選擇以分數為基礎的索引鍵型別
   - 新增您的網域
   - 設定臨界值分數（建議： 0.5）

**驗證檢查點：**&#x200B;確定您有：

- 專案 ID
- API 金鑰
- 網站金鑰
- Google Cloud中已驗證的網域

+++

+++ 步驟2：設定AEM雲端設定容器

![逐步雲端組態設定](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)
*圖：正在為您的表單容器啟用雲端設定*

**安裝程式：**

1. 存取設定瀏覽器
   - 登入您的 AEM 作者實例
   - 前往「工具>一般>設定瀏覽器」

2. 啟用雲端設定
   - 找出表單的設定容器
   - 選取屬性
   - 檢查雲端設定
   - 按一下儲存並關閉

3. 驗證設定
   - 確認容器屬性中是否顯示「雲端設定」

**驗證檢查點：**

- 為您的容器啟用的雲端設定
- 容器會顯示在設定瀏覽器中
- 屬性會將「雲端設定」顯示為已啟用

+++

+++ 步驟3：在AEM中設定reCAPTCHA Enterprise Service

![reCAPTCHA Enterprise組態畫面](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)
*圖： AEM中的reCAPTCHA企業組態介面*

**組態：**

1. 存取reCAPTCHA
   - 前往「工具>雲端服務> reCAPTCHA」
   - 選取表單的設定容器
   - 按一下建立

2. 設定企業設定值
   - 標題：描述性名稱（例如「Production reCAPTCHA」）
   - 名稱：系統名稱（自動產生或自訂）
   - 版本：選取ReCAPTCHA Enterprise
   - 專案ID：輸入您的Google Cloud專案ID
   - 網站金鑰：輸入Google Cloud的網站金鑰
   - API金鑰：輸入您的Google Cloud API金鑰
   - 索引鍵型別：選取以分數為基礎的網站索引鍵

3. 設定安全性臨界值
   - 臨界值分數：設定在0.0到1.0之間
   - 建議值：
      - 0.7-0.9：高安全性（可能會封鎖某些合法使用者）
      - 0.5-0.7：平衡式安全性（建議）
      - 0.1-0.5：較低的安全性（可讓更多使用者使用）

4. 儲存並發佈
   - 按一下「建立」以儲存設定
   - 按一下「發佈」使其可用

**驗證檢查點：**

- 已成功儲存設定
- 所有必填欄位已完成
- 已發佈且可見的設定
- 無錯誤訊息

+++

## 設定 reCAPTCHA Standard

+++步驟1：取得reCAPTCHA API金鑰（請參閱詳細資訊）

>[!IMPORTANT]
>
> Edge Delivery Services Forms僅支援reCAPTCHA v2 （以分數為基礎）。 請勿使用核取方塊版本。

**金鑰產生：**

1. 存取Google reCAPTCHA主控台

   - 移至[Google reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin)
   - 使用您的Google帳戶登入

2. 建立新網站

   - 按一下+以新增網站
   - 標籤：輸入描述性名稱
   - reCAPTCHA型別：選取reCAPTCHA v2 > 「我不是自動機制」隱藏
   - 網域：新增您的表單網域
   - 接受條款並按一下提交

3. 收集您的金鑰

   - 網站金鑰：複製網站金鑰（公開金鑰）
   - 秘密金鑰：複製秘密金鑰（私密金鑰）

**驗證檢查點：**

- 在reCAPTCHA主控台中建立的網站

- 已取得網站金鑰

- 已取得秘密金鑰

- 網域已新增並驗證

+++

+++步驟2：設定AEM雲端設定容器（請參閱詳細資訊）

遵循與「企業」設定中相同的程式：

1. 在設定瀏覽器中啟用雲端設定

2. 驗證容器設定

3. 確認設定已儲存

+++

+++步驟3：在AEM中設定reCAPTCHA標準服務（請參閱詳細資訊）

![reCAPTCHA標準組態畫面](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)
*圖： AEM中的reCAPTCHA標準組態介面*

**組態：**

1. 存取reCAPTCHA

   - 前往「工具>雲端服務> reCAPTCHA」
   - 選取表單的設定容器
   - 按一下建立

2. 設定標準設定

   - 標題：描述性名稱（例如「標準reCAPTCHA」）
   - 名稱：系統名稱（自動產生或自訂）
   - 版本：選取ReCAPTCHA v2
   - 網站金鑰：輸入您的Google reCAPTCHA網站金鑰
   - 秘密金鑰：輸入您的Google reCAPTCHA秘密金鑰

3. 儲存並發佈

   - 按一下「建立」以儲存設定
   - 按一下「發佈」使其可用

**驗證檢查點：**

- 已建立設定且沒有錯誤

- 兩個鍵都輸入正確

- 已成功發佈設定

- 設定會顯示在清單中

+++

## 將reCAPTCHA新增至您的表單

設定reCAPTCHA服務後，請依照下列步驟將保護新增至您的表單：

![正在新增reCAPTCHA元件至表單](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)
*圖：正在新增不可見的驗證碼元件至您的表單*

+++1. 在通用編輯器中開啟表單
前往AEM Sites中的表單，然後按一下「編輯」以在通用編輯器中開啟表單。 等待編輯器載入。

- 前往AEM Sites中的表格
- 按一下「編輯」以在通用編輯器中開啟
- 等待編輯器載入
+++

+++2. 找出表單結構
在內容樹狀結構（左側面板）中，尋找您的「最適化表單」區段並展開表單結構以檢視插入點。

- 在內容樹狀結構（左側面板）中，尋找您的最適化表單區段
- 展開表單結構以檢視插入點
+++

+++3. 新增reCAPTCHA元件
將驗證碼（隱藏）元件新增至您的表單。

- 按一下表單區段中的「新增(+)」圖示
- 從元件清單中，選取驗證碼（隱藏）
- 或者，從元件面板拖放元件
+++

+++4. 設定元件（可選）
選取新新增的驗證碼元件，並確認其使用您的reCAPTCHA組態。

- 選取新新增的驗證碼元件
- 在「屬性」面板中，確認其使用您的reCAPTCHA組態
- 基本設定不需要額外設定
+++

+++5. 發佈您的變更
發佈您的變更，並確認沒有錯誤。

- 按一下Universal Editor中的「發佈」
- 等待確認
- 確認未出現任何錯誤
+++

### 驗證實作

您的受保護表單現在可從以下網址取得：

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/
<form-name>
```

**範例URL：**

```
https://main--my-forms--company.aem.live/content/forms/af/
contact-us-form
```
