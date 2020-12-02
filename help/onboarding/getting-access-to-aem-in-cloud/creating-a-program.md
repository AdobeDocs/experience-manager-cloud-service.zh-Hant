---
title: 建立方案——雲端服務
description: 建立方案——雲端服務
translation-type: tm+mt
source-git-commit: 5658b2cc853ff7e6222a7f35e56527577d2c7324
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 3%

---


# 建立方案 {#create-a-program}

雲端原生解決方案為使用者提供必要的權限，以及在自助服務模型上建立程式的能力。

程式建立精靈會要求使用者提交詳細資訊，視使用者在特定客戶或組織可用內容範圍內建立程式的目標而定。

若是首次存取Cloud Manager或租用戶中沒有程式，使用者會看到「建立您的第一個Program」（程式）畫面。 ****&#x200B;如果使用者選取&#x200B;*Esc*&#x200B;或點選對話方塊，會顯示下列畫面：

![](assets/create-program1.png)


## 使用建立程式嚮導{#using-create-program-wizard}

根據使用者在特定客戶／組織可用項目群範圍內建立程式的目標，程式建立精靈會要求使用者提交一或多項詳細資訊。

![](assets/create-sandbox.png)

>[!NOTE]
>如果程式已存在，則您將看到登錄頁右上角的&#x200B;**添加程式**，如下圖所示。

![](assets/create-program-add.png)

## 建立沙箱程式{#create-sandbox-program}

請依照下列步驟建立沙盒程式：

1. 在建立程式嚮導中，選擇&#x200B;**設定沙箱**。 用戶在選擇&#x200B;**建立**&#x200B;之前提交程式名。

   ![](assets/create-sandbox.png)

1. 使用者會在登陸頁面上看到新的沙盒程式卡片，並可將滑鼠指標暫留在其上，以選取「雲端管理員」圖示，以導覽至「雲端管理員」概觀頁面。 卡片會通知使用者新建立的沙盒程式的自動設定狀態。 使用者將看到進展。

   ![](assets/program-create-setupdemo2.png)

1. 在程式設定和項目建立步驟完成後，用戶可以訪問&#x200B;**管理Git**&#x200B;連結，如下圖所示：

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >要瞭解有關使用Cloud Manager UI的自助服務Git帳戶管理訪問和管理Git儲存庫的更多資訊，請參閱[訪問Git](/help/implementing/cloud-manager/accessing-git.md)。


1. 在建立開發環境後，使用者就可以&#x200B;**存取AEM**&#x200B;連結，如下圖所示：

   ![](assets/create-program-5.png)

1. 完成部署至開發的非生產管道後，精靈會引導使用者存取AEM（開發時）或將程式碼部署至開發環境：

   ![](assets/create-program-setup-deploy.png)

   >[!NOTE]
   >您也可以從Cloud Manager概述頁面編輯、切換或新增程式，如下所示：

   ![](assets/create-program-a1.png)

## 刪除沙箱程式{#delete-sandbox-program}

Cloud Manager中&#x200B;*業務擁有者*&#x200B;或&#x200B;*部署管理員*&#x200B;角色的沙箱程式用戶可以刪除通過Cloud Manager UI設定的生產和階段環境。

>[!NOTE]
>在「生產」或「預備」上選取刪除選項，也可刪除集合中的其他項目。

刪除選項可從登陸頁面使用，如下所示：

![](assets/delete-sandbox1.png)

或,

從&#x200B;**程式概述**&#x200B;頁面選擇&#x200B;**刪除程式**&#x200B;以刪除您的沙箱程式。

![](assets/delete-sandbox2.png)


## 建立常規程式{#create-regular-program}

*Regular*&#x200B;程式是專為熟悉AEM和Cloud Manager並準備開始編寫、建立和測試程式碼的使用者而設計，其目的是將程式碼部署至「生產」。

請依照下列步驟建立一般方案：

1. 在「建立程式」嚮導中選擇「為Production **設定」以建立常規程式。**&#x200B;用戶可以接受預設程式名或在選擇&#x200B;**繼續**&#x200B;之前對其進行編輯。

   ![](assets/create-prod1.png)

1. 用戶將在螢幕上選擇要包含在程式中的解決方案，該螢幕將在上面螢幕後面顯示。



   >[!NOTE]
   >
   >以下畫面僅會針對已購買多個解決方案的客戶群顯示。 對於只購買一個解決方案的客戶，將不會顯示下列解決方案選擇畫面。

   ![](assets/set-up-prod2.png)

1. 選擇解決方案後，按一下&#x200B;**建立**。

   ![](assets/set-up-prod3.png)

1. 在登陸頁面上看到您的程式卡片後，將滑鼠指標暫留在其上，以選取Cloud Manager圖示，以導覽至Cloud Manager **Overview**&#x200B;頁面。

   ![](assets/set-up-prod4.png)

1. 主要的行動要求卡會引導使用者建立環境、建立非生產管道，最後是生產管道。
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >常規程式沒有&#x200B;**自動設定**&#x200B;功能。





