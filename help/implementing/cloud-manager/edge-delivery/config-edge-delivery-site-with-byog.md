---
title: 設定 Edge Delivery 網站以使用外部 Git 存放庫
description: 了解如何將 Edge Delivery 網站連結至私人或企業 Git 存放庫。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 1dbaef34-efa3-4287-b7b1-f60db938146d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 100%

---

# 設定 Edge Delivery 網站以使用外部 Git 存放庫

您可以設定 Edge Delivery 網站，從已加入 Cloud Manager 的任何私人 Git 存放庫提取程式碼。

**支援的 Git 供應商**

| 支援層級 | 供應商 | 備註 |
| --- | --- | --- |
| 正式發行 | • GitHub Enterprise (自行託管版本)<br>• Bitbucket (雲端版本)<br>• GitLab (雲端和自行託管版本) | 無需啟用請求即可連接 |
| Alpha 方案 | Azure DevOps (雲端版本) | [請求存取權](mailto:grp-cloudmanager_byog@adobe.com) |
| Beta 方案 | Adobe 託管的存放庫 (在 Cloud Manager 中建立) | [請求存取權](mailto:grp-cloudmanager_byog@adobe.com) |

**若要設定 Edge Delivery 網站以使用外部 Git 存放庫：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的方案。
1. 在「**[我的方案](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取已經設定 Edge Delivery Services 且您要在其中設定 Edge Delivery 網站以便使用外部 Git 存放庫的方案。
1. 在左側邊欄的「**方案**」標題之下，按一下「**![概觀圖示](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg)概觀**」。
1. 在「**方案概觀**」頁面上，按一下「**Edge Delivery**」標籤。
1. 在 **Edge Delivery 網站**&#x200B;表格中，在您想要設定為使用外部存放庫的網站之列尾按一下「![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)」，然後按一下「**自備 Git**」。
1. 在「自備 Git」對話框中，於「**存放庫名稱**」下拉式清單內，選擇具有 `READY` 狀態的 Git 存放庫，然後按一下「**確認**」。

   Cloud Manager 會傳回一次性秘密權杖。如果您重新設定網站，Cloud Manager 會產生新的秘密權杖。

1. 複製權杖並將其新增至 **helix-admin** 的網站設定中，如[自備 Git 指南](https://www.aem.live/developer/byo-git)所述。
1. 返回 Cloud Manager，在您剛設定為使用外部存放庫之網站的列尾，按一下「![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)」，再按一下「**同步程式碼**」。
1. 選擇要同步的分支，然後按一下「**同步**」。

現在任何分支上的每次提交，都會觸發自動同步。每當需要完全手動同步時，請再次使用「**同步程式碼**」。
