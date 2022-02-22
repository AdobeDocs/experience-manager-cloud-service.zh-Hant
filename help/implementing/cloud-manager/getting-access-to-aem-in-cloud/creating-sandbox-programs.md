---
title: '建立沙盒程式 '
description: 瞭解如何使用雲管理器建立您自己的沙盒程式以用於培訓、演示、POC或其他非生產目的。
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: cf6941759dfc1e50928009490c7c518a89ed093e
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 建立沙盒程式 {#create-sandbox-program}

沙盒程式通常用於培訓、運行演示、支援、POC或文檔記錄，而不是用於傳輸即時流量。

瞭解有關文檔中程式類型的詳細資訊 [瞭解程式和程式類型。](program-types.md)

## 建立沙盒程式 {#create}

按照以下步驟建立沙盒程式。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織。

1. 在Cloud Manager的登錄頁上按一下 **添加程式** 在螢幕右上角。

   ![雲管理器登錄頁](assets/first_timelogin1.png)

1. 在建立程式嚮導中，選擇 **設定沙盒**，提供程式名，然後按一下 **建立**。

   ![程式類型建立](assets/create-sandbox.png)

在安裝過程進行時，您將在登錄頁上看到一個新的沙盒程式卡，其中帶有狀態指示器。

![從概述頁建立沙盒](assets/program-create-setupdemo2.png)

## 訪問沙盒 {#access}

您可以查看沙盒設定的詳細資訊，也可以通過查看程式概述頁來訪問環境（一旦可用）。

1. 在Cloud Manager登錄頁中，按一下新建立程式上的省略號按鈕。

   ![訪問程式概述](assets/program-overview-sandbox.png)

1. 項目建立步驟完成後，您可以訪問 **訪問回購資訊** 連結，以便能夠使用git回購。

   ![程式配置](assets/create-program4.png)

   >[!TIP]
   >
   >要瞭解有關訪問和管理Git儲存庫的詳細資訊，請參閱文檔 [訪問Git。](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. 建立開發環境後，可使用 **訪AEM問** 連結以登錄AEM。

   ![訪問鏈AEM接](assets/create-program-5.png)

1. 完成非生產管道部署到開發後，嚮導將引導您訪問開發環境AEM或將代碼部署到開發環境。

   ![部署沙盒](assets/create-program-setup-deploy.png)

如果您需要隨時切換到其他程式或返回概覽頁以建立其他程式，請按一下螢幕左上角的程式名稱以顯示 **導航到** 的雙曲餘切值。

![導航到](assets/create-program-a1.png)
