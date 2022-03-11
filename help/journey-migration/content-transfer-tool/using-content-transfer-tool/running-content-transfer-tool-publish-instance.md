---
title: 在發佈實例上運行內容傳輸工具
description: 在發佈實例上運行內容傳輸工具
exl-id: 01faab94-a939-4004-b094-e9eb8f67b96e
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---

# 在發佈實例上運行內容傳輸工具 {#run-content-transfer-tool-publish-instance}

## 簡介 {#introduction}

內容傳輸工具(CTT)在將內容從源實例傳輸到目標實例之前不執行任何類型的內容分析。 例如， CTT在將內容插入發佈環境時不會區分已發佈和未發佈的內容。 遷移集中指定的任何內容都將被引入所選目標實例。 用戶能夠將遷移集插入Author實例或Publish實例或兩者。

>[!NOTE]
>建議在將內容移動到生產實例時，在源Author實例上安裝Content Transfer Tool，以將內容移動到目標Author實例，同樣，在源Publish實例上安裝Content Transfer Tool，將內容移動到目標Publish實例。 請參閱 [建議的方法](#recommended-approach) 的子菜單。

## 建議做法 {#recommended-approach}

按照以下所述的建議方法操作：

* 使用在Author實例上使用的相同版本的內容傳輸工具。

* 只需遷移一個發佈節點。 在開始提取之前，應從負載平衡器中刪除它。

* 建立遷移集時，請使用作者的AEMas a Cloud Service環境URL。

* 在接收發佈期間，不會縮小發佈層（與作者不同）。

   >[!IMPORTANT]
   >為防患於未然，請避免任何用戶啟動的寫操作，例如：
   > * 從as a Cloud Service作AEM者到在該環境中發佈的內容
   > * 發佈實例之間的用戶同步

