---
title: 通用編輯器 2025.07.09 發行說明
description: 以下是通用編輯器 2025.07.09 版發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 199ee7e11f6706773bd426c3d27236d6ea791a6c
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 29%

---


# 通用編輯器 2025.07.09 發行說明 {#release-notes}

此為通用編輯器 2025 年 7 月 9 日版本的發行說明。

>[!TIP]
>
>如需 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* [按一下容器上的&#x200B;**新增**&#x200B;工具列按鈕時，](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components)如果只允許一個元件型別，則不需要從下拉式選單中進行選取，即可立即插入它。
* [驗證標題工具列選項](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings)已置於功能切換之後，因為這在大多數情況下並不實用。
* [由於屬性面板中的多欄位不允許容器巢狀化，](/help/implementing/universal-editor/field-types.md#fields)演算常式現在會從欄位清單中篩選出巢狀容器，以防止無效的巢狀化。

## 早期採用功能 {#early-adopter}

如果您有興趣測試這些即將推出的功能並分享您的意見回饋，請透過與您的Adobe ID相關聯的電子郵件地址，傳送電子郵件給您的Adobe客戶成功經理。

### 新增RTE {#new-rte}

新的ProseMirror RTE在連結對話方塊中具有頁面選擇器，現在可在右側面板中使用。

### 還原/重做 {#undo-redo}

通用編輯器內容作者現在可以進行還原和取消復原。

* 其中包括在內容中完成的編輯、透過屬性面板完成的編輯，以及新增 (或複製)、移動和刪除區塊。
* 還原和取消復原僅限於目前瀏覽器工作階段。

## 其他改良功能 {#other-improvements}

* 已修正無法透過屬性邊欄編輯時移除單一資產參考的問題。
* 已修正屬性面板會無限載入的問題，因為資產參考會自動轉換為陣列，導致無限載入狀態。
   * 資產參考值現在會依原樣儲存，不會自動轉換為陣列。
* 已修正當模型已定義但不包含內容時，「屬性」面板未顯示欄位的問題。
   * 這會導致「屬性」面板針對空白詳細資料回應（例如空白內容片段）出現無限載入狀態。
* ESLint設定已重構為與版本9相容，包括更新的規則和外掛程式支援。

## 淘汰 {#deprecations}

* `text-input`元件現已正式淘汰。
   * 在`model-definition.json`中，使用文字元件來建立「屬性」面板的文字輸入。
