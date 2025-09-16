---
title: 表單產生器：選擇您的方法
description: 比較表單建立工具，找出建立最適化表單的正確方法。 無論您是需要範本或建立複雜表單的表單建立者，請根據您的需求選擇最佳的表單產生器。
keywords: 表單產生器， AEM forms，表單產生器，建立表單，表單製作器，調適型表單，核心元件， foundation元件， edge傳送服務，建立表單
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: choose-form-builder-guide
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 8%

---


# 表單產生器：選擇您的方法 {#choose-your-form-builder}

Adobe Experience Manager (AEM) Forms提供三種強大的表單建立方法，每種方法都針對不同的使用案例、技術需求和發佈目的地而設計。 無論您是要尋找範本的表單建立者，還是要建置複雜表單的開發人員，本指南都能協助您為您的專案選擇正確的表單產生器。

## 快速決策指南

使用本快速參考以找出最符合您需求的表單產生器：

| **如果您需要……** | **選擇** |
|-------------------|------------|
| **具有最新功能的現代化可擴充表單** | 核心元件 |
| **適用於高流量網站的快速表單** | 通用編輯器 |
| **維護現有表單或舊版整合** | 基礎元件 |
| **視覺拖放式製作** | 核心元件或通用編輯器 |
| **以試算表為基礎的表單建立** | 文件型製作 |
| **全通路傳遞（網頁、行動裝置、資訊站）** | 核心元件（搭配Headless API） |
| **自訂前端應用程式(React、Angular)** | 核心元件（搭配Headless API） |
| **完全控制表單轉譯** | 核心元件（搭配Headless API） |

## 瞭解您的表單產生器選項

AEM Forms提供三種主要的表單建立方法，每種方法都針對不同型別的表單建立者和使用案例而設計。 無論您是需要簡易的表單製作者來快速執行工作，還是需要具備適用於複雜專案的進階表單產生器功能，總有一套方法可符合您的需求：

### Foundation元件表單產生器

基礎元件代表典型的AEM Forms製作體驗。 雖然仍受支援，但主要建議維護現有表單，而非建立新表單。

**主要特性：**

- 傳統AEM製作介面
- 現有工作流程的穩定性備受肯定
- 僅限於AEM發佈
- 基本元件程式庫

### 核心元件表單產生器

核心元件提供最新AEM Forms功能，並改善效能、協助工具及彈性。 此表單產生器適合需要具有現代化功能的專業結果的表單建立者。 它支援AEM和Edge Delivery Services發佈，並會自動產生Headless表單，以用於在多個平台上的API驅動傳送。

**主要特性：**

- 現代的標準化元件
- 增強的效能與協助工具
- 彈性的發佈選項(AEM + Edge Delivery)
- 進階自訂功能
- 經得起未來考驗的架構
- 為全通道傳遞自動產生Headless表單

### 通用編輯器(Edge Delivery Services)

Universal Editor為Edge Delivery Services提供兩種強大的撰寫方法： WYSIWYG視覺化撰寫和使用試算表進行檔案式撰寫。 對於想要以卓越效能快速建立表單的使用者而言，這種表單製作方法可謂完美。

**主要特性：**

- 卓越效能（高燈塔分數）
- 兩種撰寫方法：WYSIWYG和檔案型
- 針對Edge Delivery Services最佳化
- 卓越的效能與SEO
- 快速開發和部署


## 詳細比較

### 技術功能

| **功能** | **Foundation** | **核心** | **通用編輯器** | **檔案型** |
|----------------|----------------|----------|---------------------|-------------------|
| **表單複雜性** | 基本 | 進階 | 進階 | 從簡單到中等 |
| **規則引擎** | 進階 | 進階 | 進階 | 有限 |
| **自訂元件** | ✅ | ✅ | ✅ | ✅ |
| **主題** | ✅ | ✅ | 專案層級 | 專案層級 |
| **範本** | ✅ | ✅ | 僅初始內容 |  |
| **片段** | ✅ | ✅ | ✅ | ✅ |
| **本地化** | ✅ | ✅ | 透過AEM Sites | 手動/功能 |

### 整合與提交

| **功能** | **Foundation** | **核心** | **通用編輯器** | **檔案型** |
|-------------|----------------|----------|---------------------|-------------------|
| **資料模型** | FDM、自訂 | FDM、自訂 | FDM、自訂 | 自訂 |
| **提交動作** | 多個選項 | 多個選項 | 多個選項 | 僅限試算表 |
| **預填** | ✅ | ✅ | 透過精靈 | ✅ |
| **驗證碼** | 多種型別 | reCAPTCHA、hCaptcha | reCAPTCHA Enterprise | reCAPTCHA Enterprise |
| **附件** | ✅ | ✅ | ✅ | 搶先體驗 |
| **數位簽章** | ✅ |  |  |  |

### 發佈與績效

| **外觀** | **Foundation** | **核心** | **通用編輯器** | **檔案型** |
|------------|----------------|----------|---------------------|-------------------|
| **正在發佈** | 僅限 AEM | AEM + Edge Delivery + Headless API | Edge Delivery | Edge Delivery |
| **效能** | 標準 | 已改善 | Lighthouse分數較高 | Lighthouse分數較高 |
| **SEO最佳化** | 基本 | 良好 | 極佳 | 極佳 |
| **行動回應** | 良好 | 極佳 | 極佳 | 極佳 |

## 選擇正確的產生器

### 選擇基礎元件，如果：

- 您正在維護現有的Foundation表單
- 您需要數位簽名整合
- 您的工作流程取決於已建立的基礎功能
- 您符合僅限AEM的發佈需求

**適用於：**&#x200B;表單維護、舊版系統整合、已建立的工作流程

### 選擇核心元件，如果：

- 您正在建置新的現代化表單
- 您需要彈性才能在AEM或Edge Delivery Services上發佈
- 想要最新的功能
- 您需要進階自訂與設定主題
- 協助工具與效能為優先順序
- 您想要未來可靠的技術

**適合：**&#x200B;新專案、可擴充的解決方案、現代網路體驗

### 選擇萬用編輯器，如果：

- 您需要卓越的效能與SEO
- 您正在建置Edge Delivery Services網站
- 您需要包含自訂動作的複雜表單
- 需要與外部系統整合

**適用於：**&#x200B;高效能網站、Edge Delivery Services、視覺化撰寫工作流程

### 選擇檔案式製作，如果：

- 商務使用者偏好試算表式撰寫
- 您需要快速建立原型和部署
- Forms相對簡單（調查、註冊、意見回饋）
- 試算表中的資料收集符合您的需求
- 不需要進階提交工作流程

**適用於：**&#x200B;快速部署、業務使用者編寫、簡單資料收集


## 移轉考量事項

### 從基礎到核心元件

- **建議的方法：**&#x200B;使用[移轉公用程式工具](/help/forms/migration-utility-tool-for-af-core-components.md)
- **優點：**&#x200B;現代功能、更優異的效能、雙工發佈功能
- **工作量：**&#x200B;中到高，視表單複雜度而定

### 從傳統編輯器轉換為通用編輯器

- **方法：**&#x200B;使用WYSIWYG重新建立表單，或在通用編輯器中以檔案為基礎的製作
- **優點：**&#x200B;卓越的效能、現代的開發經驗、高的SEO分數
- **工作量：**&#x200B;複雜表單為高，簡單表單為低

## 快速入門

選擇表單產生器後：

### 基礎元件

1. [建立最適化表單 (基礎元件)](/help/forms/creating-adaptive-form.md)
2. [Foundation Components編寫指南](/help/forms/introduction-forms-authoring.md)

### 核心元件

1. [建立自適應表單 (核心元件)](/help/forms/creating-adaptive-form-core-components.md)
2. [核心元件功能概觀](/help/forms/adaptive-form-core-components-json-schema-form-model.md)

### 通用編輯器(Edge Delivery Services)

1. **WYSIWYG編寫：** [通用編輯器快速入門](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
2. **檔案式製作：** [使用試算表建立您的第一個表單](/help/edge/docs/forms/tutorial.md)


## 需要協助決定嗎？

還是不確定要選擇哪個表單產生器？ 考量下列因素：

- **團隊專業知識：**&#x200B;您團隊的技術技能水準為何？
- **專案時間表：**&#x200B;您需要以多快的速度部署？
- **效能需求：**&#x200B;速度和SEO是否重要？
- **未來的擴充性：**&#x200B;您是否需要經常擴充或修改表格？
- **發佈目的地：**&#x200B;您的表單會發佈到何處？

如需個人化指引，請洽詢您的AEM Forms實作團隊或Adobe支援。

## 相關的文章

- [詳細的表單製作比較](/help/edge/docs/forms/authoring-a-form.md)
- [AEM Forms核心元件概觀](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)
- [適用於Forms的Edge Delivery Services概觀](/help/edge/docs/forms/overview.md)
- [具有核心元件的Headless最適化Forms](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service)
