---
title: 存取 Git
seo-title: 存取 Git
description: 本頁說明如何存取和管理Git存放庫。
seo-description: 請詳閱本頁，了解如何存取和管理您的Git存放庫。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 7%

---

# 存取 Git {#accessing-git}

您可以使用Cloud Manager UI中的自助服務Git帳戶管理來存取及管理您的Git存放庫。

## 使用自助服務Git帳戶管理{#self-service-git}

使用Cloud Manager UI中提供的&#x200B;**管理Git**&#x200B;按鈕，最顯眼的位於管道卡上。

1. 導覽至您的&#x200B;*方案的「概述」*&#x200B;頁面和「管道」卡。

1. 您將檢視&#x200B;**管理Git**&#x200B;選項，以存取及管理您的Git存放庫。

   ![](assets/manage-git1.png)

   此外，如果您選取&#x200B;**非生產**&#x200B;管道標籤，您也會在此檢視&#x200B;**管理Git**&#x200B;選項。

   ![](assets/manage-git-new2.png)

>[!NOTE]
>開發人員或部署管理員角色中的使用者可看見&#x200B;**管理Git**&#x200B;選項。 按一下此按鈕會開啟一個對話方塊，讓使用者可以找到Cloud Manager Git存放庫的URL及其使用者名稱和密碼。

![](assets/manage-git3.png)

在Cloud Manager中管理Git的重要考量事項包括：

* **URL**:儲存庫URL
* **使用者名稱**:使用者名稱
* **密碼**:按一下「生成密碼」 **按鈕時顯示** 的值。


>[!NOTE]
>
>使用者可以簽出其程式碼的復本，並在本機程式碼存放庫中進行變更。 準備就緒後，使用者可將其程式碼變更提交回Cloud Manager的遠端程式碼存放庫。
