---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.7.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2023.7.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 2721cb20083eeda7546513817f1ddfe12e9cb43a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 38%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.7.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 版本 2023.7.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEMas a Cloud Service中的Cloud Manager版本2023.7.0發行日期是2023年6月29日。 下一版本計畫於 2023 年 8 月 10 日發行。

## 新增功能 {#what-is-new}

* Cloud Manager 登陸頁面上的卡片現在會指出是否為其程式啟用[增強式安全性](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* 如果開發 [管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 不包含測試步驟，使用者現在可以選擇在以下情況下包含測試步驟： [啟動管道。](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#running-pipelines)
   * 這將分階段推出。
* 時間 [取消執行，](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details) 管道執行核准步驟現在會要求使用者提供取消的原因。
   * 這將分階段推出。
* 使用者現在可以存取 [複製內容程式的記錄檔。](/help/implementing/developing/tools/content-copy.md#accessing-logs)
   * 只有在來源和目的地環境皆為AEM版本時，才能使用此選項 `2023.7.12549` 或更高。

## 錯誤修正 {#bug-fixes}

* 登入後，從Cloud Manager導覽至編寫UI再也無法重新導向至Unified Shell。
* 透過上線工具集編輯上線日期現在會導覽至 **上線** 標籤而非 **增強式安全性** 標籤。
* 開始複製操作時，使用者將無法再選取已叫用複製操作的環境。
