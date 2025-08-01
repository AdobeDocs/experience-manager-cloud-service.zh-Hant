---
title: 通用編輯器 2025.07.09 版發行說明
description: 以下是通用編輯器 2025.07.09 版的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 199ee7e11f6706773bd426c3d27236d6ea791a6c
workflow-type: ht
source-wordcount: '368'
ht-degree: 100%

---


# 通用編輯器 2025.07.09 版發行說明 {#release-notes}

以下是通用編輯器 2025 年 7 月 9 日版的發行說明。

>[!TIP]
>
>如需 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* [按一下容器上的「**新增**」工具列按鈕時，](/help/sites-cloud/authoring/universal-editor/authoring.md#adding-components)如果僅允許一個元件類型，則會立即將其插入，無需從下拉式選單中選取。
* [驗證標頭工具列選項](/help/sites-cloud/authoring/universal-editor/navigation.md#autentication-settings)已放置在功能切換之後，因為此功能在大多數情況下不實用。
* [由於屬性面板中的多欄位不允許容器巢狀內嵌，](/help/implementing/universal-editor/field-types.md#fields)轉譯例行程序現在會從欄位清單中篩選掉巢狀內嵌的容器，以防止無效的巢狀內嵌。

## 早期採用功能 {#early-adopter}

如果您有興趣測試這些即將推出的功能並分享意見回饋，請使用與您 Adobe ID 相關聯的電子郵件地址，傳送電子郵件給您的 Adobe 客戶成功經理。

### 新 RTE {#new-rte}

新的 ProseMirror RTE 在連結對話框中具備頁面選擇器，現在可以在右側面板中使用。

### 還原/取消復原 {#undo-redo}

通用編輯器內容作者現在可以進行還原和取消復原。

* 其中包括在內容中完成的編輯、透過屬性面板完成的編輯，以及新增 (或複製)、移動和刪除區塊。
* 還原和取消復原僅限於目前瀏覽器工作階段。

## 其他改良功能 {#other-improvements}

* 已修正透過屬性邊欄進行編輯時，無法移除單一資產參考的問題。
* 因資產參考已自動轉換為陣列，「屬性」面板會無限期載入，造成無限載入的狀態；此問題已獲修正。
   * 資產參考值現在會按現況儲存，不會自動轉換為陣列。
* 已修正模型已定義但未包含任何內容時，「屬性」面板未顯示欄位的問題。
   * 此問題導致「屬性」面板對空的詳細資訊回應 (例如空的內容片段) 出現無限載入的狀態。
* ESLint 設定已重構，以便與版本 9 相容，包括更新的規則和外掛程式支援。

## 棄用 {#deprecations}

* `text-input` 元件現已正式棄用。
   * 在 `model-definition.json` 中，使用文字元件可建立「屬性」面板的文字輸入。
