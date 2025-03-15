---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.3.0 的發行說明
description: 了解 AEM as a Cloud Service 中 Cloud Manager 2025.3.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 5983c8579dd8606bc8bedfe6fa2a3838493452cd
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 25%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.3.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.3.0 的發行資訊。


另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.3.0發行日期是2025年3月13日星期四。

下一個預計發行日期為2025年4月10日星期四。

## 最新資訊 {#what-is-new}

* **執行多個管道**

  在管道頁面上已引入同時執行多個管道的功能。 使用者必須至少選擇一個管道，但不能超過十個。 在管道頁面的右上角附近，按一下&#x200B;**執行選取的專案(x)**。 會出現一個模型對話方塊，其中列出任何無法啟動的管道。 按一下&#x200B;**執行**&#x200B;以起始所有有效的管道。

  ![執行選取的管道對話方塊](/help/implementing/cloud-manager/release-notes/assets/run-selected-pipelines.png)

* **延伸至Node.js版本**&#x200B;的支援

  前端組建環境現在支援下列`Node.js`版本：

   * 23
   * 22
   * 20

  另請參閱[使用前端管道](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md#node-versions)開發網站。<!-- CMGR-65307 -->

<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## 錯誤修正

* Cloud Manager **中「進階網路設定」更新的**(UI)修正

  當有「可用更新」通知時，無法更新&#x200B;**進階網路設定**&#x200B;的罕見問題已解決。 之前，Cloud Manager會鎖定組態修改（包括進階網路設定），以防止在更新期間發生衝突。 客戶現在可以手動觸發擱置更新，不受限制地套用必要的變更。<!-- CMGR-65913 and CMGR-65788 -->

* **(UI)修正IP允許清單更新卡在「更新」狀態**

  解決了Cloud Manager中的IP允許清單更新由於環境的重複活動網域設定而卡在「更新」狀態的罕見問題。 以前，客戶在更新IP允許清單時會遇到無限的處理延遲，從而無法進行必要的網路存取調整。 此修正確保IP允許清單更新現在可以成功完成而不會卡住。<!-- CMGR-65786 -->




<!-- ## Known issues {#known-issues} -->
