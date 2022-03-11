---
title: 檢查IP允許清單狀態
description: 檢查IP允許清單狀態
exl-id: 5ddea04f-3720-4663-90a8-9399019bfcbe
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 檢查IP允許清單狀態 {#check-allow-list-status}

按照以下步驟確定IP允許清單更新的狀態：

1. 從中的表格中按一下「IP允許清單」的「狀態」表徵圖 **環境** 選擇 **IP允許清單** 的子菜單。

1. Cloud Manager將顯示以下狀態之一，如下節所述。

## IP允許清單的狀態 {#status}

以下是將出現在IP允許清單中的狀態定義：

* **已應用**:IP允許清單已成功應用於環境。  環境和服務可在下圖中看到。

* **更新**:正在更新IP允許清單，該清單可能包含一個或多個應用或取消應用。 每個「應用」和「取消應用」都將與「未啟動/正在進行/完成」或「失敗」一起列出。

* **失敗**:更新中的一個或多個應用或取消應用進程失敗。 每個「應用」(Apply)和「取消應用」(Unapply)將與「完成」(Complete)或「失敗」(Failed)一起列出。
   * 即使更新中的一個應用/取消應用失敗，狀態也將為「失敗」。
   * 在清除所有故障之前，狀態將保持「失敗」狀態。 用戶必須選擇狀態旁邊的重試表徵圖以清除故障。
   * 當狀態為「失敗」時，用戶將無法更新或刪除IP允許清單。

* **刪除**:刪除請求正在進行中。 這涉及取消應用所有服務。 每個取消應用將與「未啟動/正在進行/完成」或「失敗」一起列出。
完成刪除操作後，IP允許清單將：
   * IP允許清單表中不再顯示。
   * 不再對Cloud Manager程式中的任何服務應用。

* **刪除失敗**:刪除操作中的一個或多個取消應用進程失敗。 每個取消應用將與「完成」或「失敗」一起列出。

   * 即使取消應用失敗，狀態也將為「刪除失敗」。
   * 在清除所有故障之前，狀態將保持「刪除失敗」狀態。 用戶必須從 **...** 的子菜單。
   * 當狀態為「失敗」時，用戶將不被允許更新IP允許清單。

## IP允許清單的預存CDN配置 {#pre-existing-cdn}

如果客戶的環境包括IP允許清單、SSL證書或自定義域名的預先存在的CDN配置，則會在 **IP允許清單** 和 **環境** 的子菜單。 一旦客戶通過UI完全遷移了所有預先存在的環境配置，則UI上顯示的消息將消失，消息可能需要1-2個工作日才能消失。

>[!NOTE]
>為了查看和管理預先存在的配置，必須通過UI添加這些配置。 請參閱 [添加IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) 的子菜單。

![](/help/implementing/cloud-manager/assets/ip-allow-list-message1.png)

![](/help/implementing/cloud-manager/assets/ip-allow-list-message2.png)
