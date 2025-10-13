---
title: 新增 Edge Delivery 網站至 Cloud Manager
description: 了解如何將 Edge Delivery 網站新增至您的生產程式或沙箱程式。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 17e842c9-599a-4877-9834-1e7220f508a8
source-git-commit: ddf2d80330ecfddad4af8a05c95cdba7f968a986
workflow-type: ht
source-wordcount: '554'
ht-degree: 100%

---

# 新增 Edge Delivery 網站至 Cloud Manager {#adding}

>[!IMPORTANT]
>
>了解為何必須在 Cloud Manager 加入 Edge Delivery Services 網站。
>>請參閱[Edge Delivery Services 使用 Adobe 建議路徑的優勢](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#recommended-path-eds)。

**若要在 Cloud Manager 新增 Edge Delivery Site：**

1. 在 Cloud Manager 中加入 Edge Delivery Site 之前，請確保您已先使用 Edge Delivery Services 授權建立您的程式。
請參閱[建立生產程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)。
1. 在 [experiece.adobe.com](https://experience.adobe.com) 登入 Cloud Manager。
1. 在「**快速存取**」區段中，按一下「**Experience Manager**」。
1. 在左側面板中，按一下「**Cloud Manager**」。
1. 選取您想要的組織。
1. 在「**我的程式**」控制台中，按一下某個程式。
1. 執行下列任一項作業：

   * 在「**程式概觀**」頁面上，按一下「**Edge Delivery**」索引標籤。然後，在頁面右下角附近，按一下「**新增 Edge Delivery 網站**」。

     ![從「Edge Delivery」索引標籤新增 Edge Delivery 網站](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * 在頁面左上角，按一下 ![顯示選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) 以顯示左側選單。
在「**服務**」標頭下方，按一下 ![網頁頁面圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)「**Edge Delivery 網站**」。
在頁面的右上角附近按一下「![連結圖示或新增](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Link_18_N.svg)**新增 Edge Delivery 網站**」。

     ![從「Edge Delivery 網站」按鈕新增 Edge Delivery 網站](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. 在「**新增 Edge Delivery 網站**」對話框中，於必填欄位中提供以下資訊：

   | 文字欄位 | 說明 |
   | - | --- |
   | 網站名稱 | 輸入您要新增之 Edge Delivery 網站的名稱。<br>此名稱會作為該網站在 Cloud Manager 中的唯一識別碼。 |
   | Edge Delivery 來源 | 在 Edge Delivery Services 中，此值指定了您的網站內容來源的 URL 路徑。此值也會將 Cloud Manager 連結到您的上線網站。<br>該 URL 通常包括&#x200B;*分支*、*專案*&#x200B;和&#x200B;*租用戶*，如下列範例所示 (僅供參考示意)：<br>`https://main--{site}--{org}.aem.live` |
   | 網站說明 (選用) | 輸入您要新增之 Edge Delivery 網站的簡短說明。<br>說明有助於辨別和區分網站，進而更輕鬆地管理和識別您新增的其他網站。 |

1. 在對話框右下角，按一下「**新增**」。

1. 在「**驗證存放庫所有權**」對話框中，透過執行下列步驟驗證存放庫的所有權：

   | 步驟編號 | 說明 |
   | - | - |
   | **1** | 將路徑和名稱為 `well-known/adobe/cloudmanager-challenge.txt` 的檔案新增至 Git 存放庫的 `main` 分支 (列於「**存放庫 URL**」欄位中)。請&#x200B;*勿*&#x200B;在位置路徑的開頭加上句點。<br>如有需要，請按一下![複製圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)以複製路徑至剪貼簿。 |
   | **2** | 將步驟 2 文字欄位中顯示的程式碼，新增至您剛剛在步驟 1 建立的檔案中。<br>如有需要，請按一下![複製圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)以複製程式碼至剪貼簿。 |
   | **3** | 在 Git 存放庫中為您剛建立的變更建立一項提取請求，然後將其合併到 `main` 以提交程式碼。 |

1. 按一下「**驗證**」。

當存放庫通過驗證，它在 Edge Delivery 網站表格中的狀態就會更新。內有白色核取記號的綠色圓圈表示該狀態。

在同一個表格中，按一下![Edge Delivery 網站相關資訊圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg)以檢視網站詳細資訊。此資訊包括通過驗證的存放庫 URL，以及預覽和生產網站 URL。
