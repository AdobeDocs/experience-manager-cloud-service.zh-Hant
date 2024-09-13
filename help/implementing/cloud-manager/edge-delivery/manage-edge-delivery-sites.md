---
title: 在Cloud Manager中管理Edge Delivery網站
description: 瞭解如何將CDN設定新增至Edge Delivery網站或刪除Edge Delivery網站。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 在Cloud Manager中管理Edge Delivery網站 {#manage-edge-delivery-sites}

瞭解如何將CDN設定新增至現有網站，以在Cloud Manager中管理Edge Delivery網站。 或者，刪除Edge Delivery網站。

## 將CDN設定新增至現有的Edge Delivery站台 {#add-cdn-to-edge-delivery-site}

請參閱[新增CDN組態](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)。

## 刪除Edge Delivery網站 {#delete-edge-delivery-site}

如果您刪除Edge Delivery Services網站，則會一併移除任何相關聯的CDN設定。 此動作會中斷自訂網域與網站之間的連線。 如需詳細資訊，請參閱CDN設定。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**若要刪除Edge Delivery網站：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登入Cloud Manager並選取適當的程式。
1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取已設定Edge Delivery Services的程式，您要在此新增Edge Delivery網站。
1. 執行下列任一項作業：
   * 從&#x200B;**計畫總覽**&#x200B;頁面，按一下&#x200B;**Edge Delivery**標籤。 在Edge Delivery網站表格中，按一下您要移除其網站的列末尾的省略符號。
按一下[刪除]****，然後再按一下[刪除]****&#x200B;以確認移除網站。

     ![從Edge Delivery索引標籤新增Edge Delivery網站](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * 在頁面的左上角，按一下漢堡圖示以顯示左側導覽功能表。 在&#x200B;**服務**&#x200B;標題下，按一下&#x200B;**Edge Delivery網站**。
在Edge Delivery網站表格中，按一下您要移除其網站的列末尾的省略符號。 按一下[刪除]****，然後再按一下[刪除]****&#x200B;以確認移除網站。


     ![從Edge Delivery Sites按鈕](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)新增Edge Delivery網站