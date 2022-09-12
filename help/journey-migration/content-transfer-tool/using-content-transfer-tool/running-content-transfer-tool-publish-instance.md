---
title: 在發佈執行個體上執行內容轉移工具
description: 在發佈執行個體上執行內容轉移工具
exl-id: 01faab94-a939-4004-b094-e9eb8f67b96e
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# 在發佈執行個體上執行內容轉移工具 {#run-content-transfer-tool-publish-instance}

## 簡介 {#introduction}

內容轉移工具(CTT)在將內容從來源例項轉移至目標例項之前，不會執行任何類型的內容分析。 例如，CTT不會在將內容擷取至發佈環境時，區分已發佈和未發佈的內容。 無論移轉集中指定什麼內容，都會擷取至選取的目標例項。 使用者能將移轉集內嵌至製作例項、發佈例項或兩者。

>[!NOTE]
>建議在將內容移至生產例項時，在來源製作例項上安裝內容轉移工具，以將內容移至目標製作例項，同樣地，在來源發佈例項上安裝內容轉移工具，將內容移至目標發佈例項。 請參閱 [建議方法](#recommended-approach) 一節以取得詳細資訊。

## 建議做法 {#recommended-approach}

請遵循以下說明的建議方法：

* 使用與Author例項上使用相同版本的「內容轉移工具」。

* 只需移轉單一發佈節點。 在開始提取之前，應從負載平衡器中移除它。

* 擷取至發佈期間，發佈層級不會縮小（與作者不同）。

   >[!IMPORTANT]
   >為了防患於未然，請避免任何用戶啟動的寫操作，例如：
   > * 從AEMas a Cloud Service作者發佈至該環境中發佈的內容
   > * 發佈執行個體之間的使用者同步

