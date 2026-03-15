---
title: 重構工具概觀
description: 瞭解如何開始使用AEM重構工具
exl-id: b8137e01-87e8-4298-b0cc-b376330cb730
source-git-commit: 879f4f3476ee369554188d6e3b7973d32454ed4b
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

<!-- Alexandru: temporarily commeting this out, since it breaks validation

>[!CONTEXTUALHELP]
>id="aemcloud_rs_overview"
>title="Overview"
>abstract="Refactoring Tools is a solution developed by Adobe to help refactor existing AEM projects for compatibility with AEM as a Cloud Service. The tools are executed via Cloud Acceleration Manager (CAM) and automate key modernization tasks."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/guidelines-best-practices-content-transfer-tool.html?lang=zh-Hant" text="Guidelines and Best Practices"

-->

# 重構工具概觀 {#refactoring-tools-overview}

**重構工具**&#x200B;簡化更新現有AEM專案以與&#x200B;**AEM as a Cloud Service (AEMaaCS)**&#x200B;相容的程式。 這些工具可自動執行常見的重構和現代化工作，並與&#x200B;**Cloud Acceleration Manager (CAM)**&#x200B;整合，提供順暢的體驗。

「重構工具」先前僅以CLI公用程式的形式提供，現在可提供具有自動化檢查、組態產生及工作執行等功能的統一介面，減少手動開銷並提升可見度。

## 檢查工作流程 {#inspection-workflow}

**檢查工作流程**&#x200B;簡化了執行重構工具的準備程式。

### 主要功能：

* **自動觸發程式** — 上傳專案會自動開始檢查。
* **組態產生** — 工具會檢查上傳的原始程式碼並產生必要的組態。
* **裝載提交** — 這些設定會直接傳遞至選取的工具以供執行。

## 可用的重構工具

### 存放庫現代化工具 {#repo-modernizer}

**Repository Modernizer**&#x200B;會重新建構您的AEM專案的存放庫配置和內容，以符合AEMaaCS標準和最佳實務。 以增強的自動化和準確性取代舊版存放庫現代化工具。

### 程式碼轉換器 {#code-transformer}

**程式碼轉換器**&#x200B;使用智慧型模式辨識和AI驅動的分析，偵測並更新與AEMaaCS不相容的程式碼區段。 此工具可簡化移轉工作，並減少手動程式碼變更。

## 重構工作流程階段 {#phases-in-refactoring-tools}

「重構工具」遵循結構化的兩階段流程：

### 階段1：上傳Source程式碼

* 使用CAM介面上傳原始程式碼（ZIP格式）。
* 上傳之後，會自動觸發&#x200B;**檢查工作流程**，以分析專案並準備工具執行。

>[!NOTE]
>在檢查程式期間，不允許上傳其他專案。

### 階段2：觸發重構工作

檢查成功後，您可以執行一或多個重構工具：

* **執行儲存庫現代化工具** — 執行儲存庫現代化。
* **執行程式碼轉換器** — 根據檢查輸出執行程式碼轉換。
* **一起執行所有工具** — 在單一操作中執行所有可用的工具。

>[!NOTE]
>重構工作只能在成功上傳和檢查原始程式碼後開始。

>[!NOTE]
>使用者可以平行觸發多個重構作業，但每個作業將分別執行。
