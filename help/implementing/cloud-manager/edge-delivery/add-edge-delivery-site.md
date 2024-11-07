---
title: 新增 Edge Delivery 網站至 Cloud Manager
description: 瞭解如何將Edge Delivery網站新增到您的生產計畫或沙箱計畫。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 17e842c9-599a-4877-9834-1e7220f508a8
source-git-commit: db661281831dcb07491dca16e73e835b487814a6
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

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

   * 在頁面的左上角，按一下![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以顯示左側功能表。
在**服務**&#x200B;標題下，按一下![網頁圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery網站**。
在頁面的右上角附近，按一下**新增網站**。

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
   | **1** | 將路徑和名稱為`well-known/adobe/cloudmanager-challenge.txt`的檔案新增至&#x200B;**存放庫URL**&#x200B;欄位中所列之Git存放庫的`main`分支。 請&#x200B;*不*&#x200B;在位置路徑的開頭新增句號。<br>如有必要，請按一下[複製]，將路徑複製到剪貼簿。![](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) |
   | **2** | 將步驟2中在文字欄位中看到的程式碼新增至您在步驟1中剛建立的檔案。<br>如有必要，請按一下[複製]，將代碼複製到剪貼簿。![](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) |
   | **3** | 在Git存放庫中為您剛才建立的變更建立提取請求，然後將其合併到`main`以認可程式碼。 |

1. 按一下&#x200B;**驗證**。

驗證存放庫後，其在Edge Delivery網站表格中的狀態會更新。 內部帶有白色勾號的綠色圓圈表示狀態。

在相同表格中，按一下![Edge Delivery網站的相關資訊](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg)以檢視網站詳細資訊。 此資訊包括已驗證的存放庫URL，以及預覽和生產網站URL。
