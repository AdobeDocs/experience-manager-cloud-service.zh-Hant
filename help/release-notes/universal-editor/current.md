---
title: Universal Editor 2024.08.13發行說明
description: 這些是2024.08.13版通用編輯器的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: d71d3481004f2429c018c536b3e12784cf597f85
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---


# Universal Editor 2024.08.13發行說明 {#release-notes}

這些是2024年8月13日發行的Universal Editor的發行說明。

>[!TIP]
>
>如需Adobe Experience Manager as a Cloud Service目前的發行說明，請參閱[此頁面。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* **自訂資料型別**：根據您的獨特資料需求量身打造編輯器，並能在屬性面板中建立自訂欄位。
   * 無論您是開發商務使用案例的自訂產品選擇器，還是使用您後端的值填入下拉式清單，此功能都可讓您控制作者用來撰寫內容的資料。
* **跨容器拖放**：您可以透過拖放至[內容樹狀結構面板中的方式，跨不同容器移動元件，讓版面組合更加靈活。](/help/sites-cloud/authoring/universal-editor/navigation.md#content-tree-mode)
* **最佳化的GitHub整合**：已引入GitHub回應的快取，大幅加快標籤和`universal-editor-cors-library`的擷取速度，進而提供更快速且流暢的使用者體驗。
* **Managed Services RPM套件**：Adobe現在提供RPM套件，以簡化Universal Editor Service的部署和管理，簡化維護作業，並減少Managed Services的作業額外負荷。
* **可設定的IMS權杖驗證**：若要增加權杖管理的彈性，現在可選擇IMS權杖驗證。
   * 此設定選項可讓您視需要停用驗證，進而簡化雲端閘道的設定。
* **Splunk整合**： Splunk記錄已整合至Universal Editor Service Express，可加強監控和診斷。
   * 此整合可確保有效率的記錄追蹤、更順暢的操作，以及更快的疑難排解。

## 錯誤修正 {#bug-fixes}

* **增強型發佈意見反應**：如果因許可權不足而發佈失敗，則發佈期間對使用者的意見反應已改善為顯示清楚的警告，而非單純表示失敗。
* **已改善URL處理**：已修正造成發佈失敗的URL編碼/解碼錯誤問題。
* **正確的資料處理**：已解決浮點數錯誤地儲存為整數的問題，以確保整個內容的精確資料處理。
* **安全性與穩定性**： Docker映像中的安全性弱點已修正，重要元件（例如元件選擇器和階層連結）的測試涵蓋範圍已實施，進而提供更安全、穩定且可靠的編輯器體驗。
