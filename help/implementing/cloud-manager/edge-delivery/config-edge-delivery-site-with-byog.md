---
title: 設定Edge Delivery網站以使用外部Git存放庫
description: 瞭解如何將Edge Delivery網站連結至私人或企業Git存放庫。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 239ee3021057dd108d18ab2d7729680692223403
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 7%

---


# 設定Edge Delivery網站以使用外部Git存放庫

您可以設定Edge Delivery網站，從任何已上線至Cloud Manager的私人Git存放庫提取程式碼。

**支援的Git廠商**

| 支援等級 | 廠商 | 備註 |
| --- | --- | --- |
| 全面發佈 | · GitHub Enterprise （自我託管版本）<br>· Bitbucket （雲端版本）<br>· GitLab （雲端和自託管版本） | 無需啟用請求即可連線 |
| Alpha程式 | Azure DevOps （雲端版本） | [要求存取權](mailto:grp-cloudmanager_byog@adobe.com) |
| Beta程式 | Adobe託管的存放庫(建立於Cloud Manager) | [要求存取權](mailto:grp-cloudmanager_byog@adobe.com) |

**若要設定Edge Delivery網站使用外部Git存放庫：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的程式。

1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，選取已設定Edge Delivery Services的程式，其中您想要設定Edge Delivery網站使用外部Git存放庫。

1. 在左側邊欄的&#x200B;**方案**&#x200B;標題下，按一下&#x200B;**![總覽圖示](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg)總覽**。

1. 在&#x200B;**方案概觀**&#x200B;頁面上，按一下「**Edge Delivery**」索引標籤。

1. 在&#x200B;**Edge Delivery網站**&#x200B;表格中，按一下您要設定其網站以使用外部存放庫之資料列結尾的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後按一下&#x200B;**自備Git**。

1. 在「自備Git」對話方塊的&#x200B;**存放庫名稱**&#x200B;下拉式清單中，選擇狀態為`READY`的Git存放庫，然後按一下&#x200B;**確認**。

   Cloud Manager會傳回一次性密碼Token。 如果您重新設定網站，Cloud Manager會產生新的秘密代號。

1. 複製Token並新增至&#x200B;**helix-admin**&#x200B;中的網站設定，如[BYO Git指南](https://www.aem.live/developer/byo-git)所述。

1. 返回Cloud Manager，按一下您剛設定使用外部存放庫之網站所在列結尾的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然後按一下&#x200B;**同步程式碼**。

1. 挑選要同步的分支，然後按一下&#x200B;**同步**。

任何分支上的每次認可現在都會觸發自動同步。 當需要完全手動同步處理時，請再次使用&#x200B;**同步處理程式碼**。

