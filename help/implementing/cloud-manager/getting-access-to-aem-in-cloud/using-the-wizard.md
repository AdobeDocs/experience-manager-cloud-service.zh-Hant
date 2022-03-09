---
title: 項目建立嚮導
description: 瞭解項目建立嚮導，以幫助您在建立生產程式後快速設定項目。
exl-id: 03736ca7-1345-4faf-a61a-f9213ab5c89a
source-git-commit: 93cb0ffa87f2338518c2a23de4e0a692031e1a71
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# 項目建立嚮導 {#project-creation-wizard}

建立生產程式後，Cloud Manger將提供一個嚮導，以根AEM據 [項AEM目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 快速啟動。

按照以下步驟使AEM用嚮導在Cloud Manager中建立應用程式項目。

1. 按照文檔中的步驟建立生產程式 [建立生產程式](creating-production-programs.md)

1. 程式設定完成後，訪問 **概述** 程式螢幕並查看 **建立分支和項目** 行動呼叫卡。

   ![嚮導的行動要求](assets/create-wizard1.png)

1. 按一下 **建立** 啟動嚮導並確認項目 **標題** 和 **新建分支名稱** 的 **建立分支和項目** 的子菜單。

   ![建立分支和項目](assets/create-wizard2.png)

1. 或者，按一下分隔線以顯示項目的附加參數。 預設值由「項目原型」AEM提供，通常不需要更改。

   ![其他項目參數](assets/create-wizard5.png)

1. 按一下 **建立** 的子菜單。


A **正在建立項目** 卡現在取代了 **建立分支和項目** 行動呼叫卡作為 **計畫概述** 的上界。

![正在建立項目](assets/create-wizard3.png)

程式建立完成後， **添加環境** 卡取代了 **正在建立項目** 卡在頂部 **計畫概述** 的上界。

![添加環境](assets/create-wizard4.png)

現在，您的AEMGit儲存庫AEM中添加了基於原型的項目，以作為您自己項目的開發基礎。 接下來，您可以建立可在其中部署項目代碼的環境。

請參閱文檔 [管理您的環境](/help/implementing/cloud-manager/manage-environments.md) 瞭解如何添加或管理環境。

>[!NOTE]
>
>該嚮導僅可用於生產程式。 因為 [沙盒程式](introduction-sandbox-programs.md#auto-creation) 包括自動建立項目，不必使用嚮導。