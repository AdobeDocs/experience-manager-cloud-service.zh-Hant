---
title: Universal Editor 2024.06.28發行說明
description: 這些是2024.06.28版通用編輯器的發行說明。
feature: Release Information
role: Admin
source-git-commit: cc94ad2ba42707bb7541217f0225b995f64ad84f
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 1%

---


# Universal Editor 2024.06.28發行說明 {#release-notes}

這些是2024年6月28日發行的Universal Editor的發行說明。

>[!TIP]
>
>如需Adobe Experience Manager as a Cloud Service的目前發行說明，請參閱 [此頁面。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* **首頁**：最近使用的頁面會顯示為清單，沒有預覽影像。
* **位置列**：新增了增強型URL驗證，強制執行HTTPS URL並支援URL中的雜湊，以處理雜湊路由的應用程式。
* **鍵盤導覽**：頁面覆蓋選取範圍與屬性邊欄焦點脫離，以改善頁面上的鍵盤導覽，而不會失去焦點。
* **專案標籤**：標籤現在使用的遞補值 `data-aue-prop` 而非 `data-aue-type` 以便在覆蓋圖和內容樹中更清楚識別。
* **RTE強制回應視窗**：A **取消** 從「屬性」面板開啟RTF編輯器強制回應視窗時，按鈕已新增到該視窗中。
* **節點上的UE服務**：重新推出Universal Editor服務的HTTP支援，因為所有HTTPS連線都會在Dispatcher層級終止。
* **內部複製API**：已新增通用編輯器服務的API來複製元件，以便未來推出工具列選項來複製和複製內容。

## 錯誤修正 {#bug-fixes}

* **屬性面板階層連結**：已修正深層巢狀專案屬性面板中的階層連結功能表（並未維持開啟狀態）。
* **內容片段選擇器**：內容片段選擇器已經過改良，以確保其遵守內容片段模式中或 `data-aue-filter`.
* **元件插入**：已更正插入新元件的清單（在導覽至其他頁面後未正確更新）。
* **發佈狀態**：改善發佈狀態的處理方式，以更一致地運作。
* **其他修正**：此版本也包含各種微幅修正、技術債務清理、安全性增強，以及整體穩定性和效能的整合測試。
