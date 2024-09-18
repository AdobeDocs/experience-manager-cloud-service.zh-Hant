---
title: 將Edge Delivery網站新增至Cloud Manager
description: 瞭解如何將Edge Delivery網站新增到您的生產計畫或沙箱計畫。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ad6a0e13f27839b9900e440d60948158ddf75d99
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 3%

---


# 將Edge Delivery網站新增至Cloud Manager {#adding}

將Edge Delivery網站新增至生產程式後，您的Edge Delivery Services授權即會套用至該網站。

必須將Edge Delivery網站新增至Cloud Manager，才能[註冊Edge Delivery專案的支援票證](/help/edge/overview.md##support-ticket)。

另請參閱[Cloud ManagerEdge Delivery Services簡介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

**若要將Edge Delivery網站新增至Cloud Manager：**

1. 在[`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/)登入Cloud Manager並選取適當的程式。
1. 執行下列任一項作業：

   * 從&#x200B;**計畫總覽**&#x200B;頁面，按一下&#x200B;**Edge Delivery**&#x200B;標籤。 然後，在頁面的右下角附近，按一下&#x200B;**新增Edge Delivery網站**。

     ![從Edge Delivery索引標籤新增Edge Delivery網站](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * 在頁面的左上角，按一下漢堡圖示以顯示左側導覽功能表。 在&#x200B;**服務**&#x200B;標題下，按一下&#x200B;**Edge Delivery網站**。 在頁面的右上角附近，按一下&#x200B;**新增網站**。

     ![從Edge Delivery Sites按鈕](/help/implementing/cloud-manager/assets/cm-eds-add2.png)新增Edge Delivery網站

1. 在&#x200B;**新增Edge Delivery網站**&#x200B;對話方塊中，在必要欄位中提供下列資訊：

   | 文字欄位 | 說明 |
   | - | --- |
   | 網站名稱 | 輸入您要新增的Edge Delivery網站名稱。<br>此名稱可作為Cloud Manager中網站的唯一識別碼。 |
   | 存放庫 URL | 輸入儲存網站程式碼的Git存放庫。<br>此欄位可讓Cloud Manager在部署程式期間從該存放庫提取程式碼。 |
   | 網站說明 (可選) | 輸入您要新增之Edge Delivery網站的簡短說明。<br>說明可協助識別並區分網站，讓您更容易管理和識別您所新增的其他網站。 |

1. 在對話方塊的右下角，按一下&#x200B;**新增**。

1. 在&#x200B;**驗證存放庫擁有權**&#x200B;對話方塊中，執行下列步驟來驗證您的存放庫擁有權：

   | 步驟編號 | 說明 |
   | - | - |
   | **1** | 將路徑和名稱為`well-known/adobe/cloudmanager-challenge.txt`的檔案新增至&#x200B;**存放庫URL**&#x200B;欄位中所列之Git存放庫的`main`分支。 請&#x200B;*不*&#x200B;在位置路徑的開頭新增句號。<br>如有需要，請按一下&#x200B;**複製**&#x200B;圖示，將路徑複製到剪貼簿。 |
   | **2** | 將步驟2中在文字欄位中看到的程式碼新增至您在步驟1中剛建立的檔案。<br>如有需要，請按一下&#x200B;**複製**&#x200B;圖示，將程式碼複製到剪貼簿。 |
   | **3** | 在Git存放庫中為您剛才建立的變更建立提取請求，然後將其合併到`main`以認可程式碼。 |

1. 按一下&#x200B;**驗證**。

驗證存放庫後，其在Edge Deliver Sites表格中的狀態會變更為綠色圓形，且內有白色勾號。
