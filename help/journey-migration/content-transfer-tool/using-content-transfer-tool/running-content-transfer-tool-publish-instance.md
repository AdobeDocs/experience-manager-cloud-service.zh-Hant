---
title: 在發佈執行個體上執行內容轉移工具
description: 在發佈執行個體上執行內容轉移工具
exl-id: 01faab94-a939-4004-b094-e9eb8f67b96e
feature: Migration
role: Admin
source-git-commit: 4408f15ef85d0fc2c6a0e2b45038dc900d212187
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 11%

---

# 在發佈執行個體上執行內容轉移工具 {#run-content-transfer-tool-publish-instance}

## 簡介 {#introduction}

在將內容從來源例項轉移至目標例項之前，內容轉移工具(CTT)不會執行任何型別的內容分析。 例如，將內容擷取至Publish環境時，CTT不會區分已發佈和未發佈的內容。 移轉集中指定的任何內容都會擷取到所選的目標例項。 使用者能將移轉集擷取至作者執行個體或Publish執行個體（或兩者）。

>[!NOTE]
>建議在將內容移至生產執行個體時，在來源製作執行個體上安裝「內容轉移工具」，將內容移至目標製作執行個體，並在來源Publish執行個體上安裝「內容轉移工具」，將內容移至目標Publish執行個體。 如需詳細資訊，請參閱下面的[建議方法](#recommended-approach)部分。

## 建議做法 {#recommended-approach}

請遵循下述建議方法：

* 使用與Author例項上使用的「內容轉移工具」相同版本。

* 僅能移轉單一發佈節點。 在開始擷取之前，應將其從負載平衡器中移除。

* 在擷取至發佈期間，發佈層級將不會縮小（不像作者）。

  >[!IMPORTANT]
  >為防萬一，請避免任何使用者啟動的寫入操作，例如：
  > * 在該環境中從AEM as a Cloud Service Author到Publish的內容發佈
  > * 發佈執行個體之間的使用者同步
