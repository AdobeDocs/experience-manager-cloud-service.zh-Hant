---
title: 通用編輯器 2025.02.17 發行說明
description: 此文件為通用編輯器 2025.02.17 版本的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: af04ad7e3f89247580c48c276cb371d78ac56a49
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 22%

---


# 通用編輯器 2025.02.17 發行說明 {#release-notes}

這些是2025年2月17日發行的Universal Editor的發行說明。

>[!TIP]
>
>如需 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* **發佈到預覽** — 使用通用編輯器發佈（或取消發佈）內容時，您現在可以選擇是否除了發佈環境之外，還希望發佈到預覽環境
   * 這可讓您在公開發行之前先檢閱內容。
* **可在元件定義中定義模型和篩選器** — 您現在可以定義元件定義中要使用的模型和篩選器。
   * 這些資訊可在定義中集中維護，不需要在檢測中指定。
   * 這可讓您跨容器移動元件。
* **容器的子專案會隱含地視為元件** — 如果將具有`data-aue-resource`的專案作為直接子專案放入容器中，則會將其視為元件，且移動時不必指定`data-aue-behavior="component"`。

## 其他改善功能 {#other-improvements}

* **AEM 6.5資產選擇器** — 透過AEM 6.5執行通用編輯器時，6.5資產選擇器現在會正常開啟。

