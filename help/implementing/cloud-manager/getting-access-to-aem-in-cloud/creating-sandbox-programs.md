---
title: 建立沙箱方案
description: 了解如何使用Cloud Manager建立您自己的沙箱計畫，以用於訓練、示範、POC或其他非生產用途。
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: cf6941759dfc1e50928009490c7c518a89ed093e
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# 建立沙箱方案 {#create-sandbox-program}

沙箱計畫通常是為了提供培訓、執行示範、培訓、POC或檔案等目的而建立，且用途不是承載即時流量。

進一步了解檔案中的方案類型 [了解方案和方案類型。](program-types.md)

## 建立沙箱方案 {#create}

請依照下列步驟建立沙箱方案。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 在Cloud Manager的登陸頁面上按一下 **添加程式** 在畫面的右上角。

   ![Cloud Manager登陸頁面](assets/first_timelogin1.png)

1. 在建立程式嚮導中，選擇 **設定沙箱**，請提供方案名稱，然後按一下 **建立**.

   ![程式類型建立](assets/create-sandbox.png)

隨著設定程式的進行，您會在登陸頁面上看到新的沙箱方案卡片，其中包含狀態指標。

![從概述頁面建立沙箱](assets/program-create-setupdemo2.png)

## 存取您的沙箱 {#access}

您可以檢視沙箱設定的詳細資訊，並透過檢視方案概觀頁面來存取環境（一旦可用）。

1. 從Cloud Manager登陸頁面，按一下新建立的程式上的刪節號按鈕。

   ![存取方案概觀](assets/program-overview-sandbox.png)

1. 專案建立步驟完成後，您可以存取 **存取存放庫資訊** 連結，以便使用您的git存放庫。

   ![程式配置](assets/create-program4.png)

   >[!TIP]
   >
   >若要進一步了解如何存取及管理Git存放庫，請參閱本檔案 [存取Git。](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. 建立開發環境後，您就可以使用 **存取AEM** 連結以登入AEM。

   ![存取AEM連結](assets/create-program-5.png)

1. 完成部署至開發的非生產管道後，精靈就會引導您存取AEM開發環境或將程式碼部署至開發環境。

   ![部署沙箱](assets/create-program-setup-deploy.png)

如果您隨時需要切換至其他程式或返回概覽頁面以建立其他程式，請按一下畫面左上角的程式名稱以顯示 **導覽至** 選項。

![導航到](assets/create-program-a1.png)
