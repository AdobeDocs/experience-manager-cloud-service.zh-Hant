---
title: 通用編輯器 2025.06.19 發行說明
description: 以下是通用編輯器 2025.06.19 版本的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 5ffae9e548ca952975b3ea805808e227102ec99f
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 31%

---


# 通用編輯器 2025.06.19 發行說明 {#release-notes}

此文件為通用編輯器 2025 年 6 月 19 日版本的發行說明。

>[!TIP]
>
>如需 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **屬性邊欄中的多重欄位支援** -
  [容器元件](/help/implementing/universal-editor/field-types.md#container)現在可用來建立多欄位屬性。
* **支援巢狀屬性** - [`name`欄位](/help/implementing/universal-editor/field-types.md#nesting)現在支援啟用屬性巢狀化的路徑。
* **可調整大小的右側面板** — 現在可以調整側邊面板的大小，以更能說明側邊面板中顯示的較長時間內容。

## 早期採用功能 {#early-adopter}

為了有機會測試一些即將推出的功能，請加入Adobe的早期採用者計畫。

### **還原/重做** {#undo-redo}

「通用編輯器」內容作者現在可以使用「復原」和「重做」 。

* 其中包括在內容中完成的編輯、透過「屬性」面板完成的編輯，以及新增（或複製）、移動和刪除區塊。
* 還原和重做僅限於目前的瀏覽器作業階段。

如果您有興趣測試此新功能並分享意見反應，請使用與您 Adobe ID 相關聯的電子郵件地址，傳送電子郵件給您的 Adobe 客戶成功經理。

## 其他改良功能 {#other-improvements}

* 已修正容器之間移動區塊時的資源金鑰衝突錯誤。
* 已修正導致複製容器的最後一個區塊失敗的問題。
* 「新增動作」下拉式清單現在只會列出在`component-definition.json`檔案中定義合適外掛程式的元件。
* 發佈對話方塊使用的修改日期已修正，其中某些情況下頁面無法辨識為已修改，且無法重新發佈。
* 修正編輯容器時取消子節點繼承的MSM繼承行為。
* `fetchUrl`已修正，正在將移動區塊從一個容器還原至另一個容器。
