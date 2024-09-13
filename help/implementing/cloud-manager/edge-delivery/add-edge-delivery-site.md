---
title: 將Edge Delivery網站新增至Cloud Manager
description: 瞭解如何將Edge Delivery網站新增到您的生產計畫或沙箱計畫。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 2%

---


## 將Edge Delivery網站新增至Cloud Manager {#eds-add-site}

將Edge Delivery Services新增到生產計畫後，您的Edge Delivery Services授權將套用到該計畫。

概觀頁面上顯示名為&#x200B;**Edge Delivery**&#x200B;的可點按索引標籤。 按一下索引標籤會顯示一個表格，其中列出您已新增的每個Edge Delivery網站。 在左側導覽面板的&#x200B;**服務**&#x200B;群組下方，請注意名為&#x200B;**Edge Delivery Sites**&#x200B;的功能表選項。

![總覽頁面在左側導覽面板中顯示Edge Delivery Sites，並在Edge Delivery索引標籤右側顯示Publish傳送索引標籤](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**若要將Edge Delivery網站新增至Cloud Manager：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登入Cloud Manager並選取適當的程式。
1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取已設定Edge Delivery Services的程式，您要在此新增Edge Delivery網站。
1. 執行下列任一項作業：
   * 從&#x200B;**計畫總覽**&#x200B;頁面，按一下&#x200B;**Edge Delivery**&#x200B;標籤。 然後，在頁面的右下角附近，按一下&#x200B;**新增Edge Delivery網站**。

     ![從Edge Delivery索引標籤新增Edge Delivery網站](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     **Edge Delivery待辦事項清單** （如上圖所示）是選用的入門檢查清單指南，可協助您開始使用Edge Delivery。 請參閱[關於Edge Delivery待辦事項清單](#ed-todo-list)。

   * 在頁面的左上角，按一下漢堡圖示以顯示左側導覽功能表。 在&#x200B;**服務**&#x200B;標題下，按一下&#x200B;**Edge Delivery網站**。 在頁面的右上角附近，按一下&#x200B;**新增網站**。

     ![從Edge Delivery Sites按鈕](/help/implementing/cloud-manager/assets/cm-eds-add2.png)新增Edge Delivery網站

1. 在&#x200B;**新增Edge Delivery網站**&#x200B;對話方塊中，執行下列動作：

   | 文字欄位 | 該做什麼 |
   | --- | --- |
   | 網站名稱 | 輸入您要新增的Edge Delivery網站名稱。 此名稱可作為Cloud Manager中網站的唯一識別碼。 |
   | 存放庫 URL | 此欄位是指儲存網站程式碼的Git存放庫。<br>輸入Git存放庫的URL，此存放庫包含您Edge Delivery網站所需的檔案和資源(例如HTML、CSS、JavaScript和其他網頁資產)。 這種安排可讓Cloud Manager在部署程式期間從該存放庫提取計畫碼。 |
   | 網站說明 (可選) | 輸入您要新增之Edge Delivery網站的簡短說明。<br>此描述可協助識別並區分網站，讓您更容易管理和識別您新增的其他網站。 您可能會想要加入有關網站用途、內容的詳細資訊，或任何其他可協助釐清其功能或範圍的相關資訊。 |

1. 在對話方塊的右下角，按一下&#x200B;**新增**。

1. 在&#x200B;**驗證存放庫擁有權**&#x200B;對話方塊中，執行下列各項：

   | 步驟 | 說明 |
   | --- | --- |
   | 1 | 將具有位置路徑的檔案新增至&#x200B;**存放庫URL**&#x200B;欄位中列出的Git存放庫的`main`分支。 如有必要，請按一下「複製」圖示，將路徑複製到剪貼簿。<br>位置路徑為：<br>`well-known/adobe/cloudmanager-challenge.txt`。<br><br>請&#x200B;*不*&#x200B;在位置路徑的開頭新增句號，位於：<br>`.well-known/adobe/cloudmanager-challenge.txt` |
   | 2 | 將產生的程式碼新增至您在步驟1建立的檔案中。 如有必要，請按一下「複製」圖示，將程式碼複製到剪貼簿。 |
   | 3 | 在Git存放庫中，建立提取請求，然後將其合併以認可程式碼。 |

1. 按一下&#x200B;**驗證**。 驗證存放庫後，其在Edge Deliver Sites表格中的狀態會變更為綠色圓形，且內有白色勾號。
