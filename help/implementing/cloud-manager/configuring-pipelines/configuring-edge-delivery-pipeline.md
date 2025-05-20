---
title: 新增Edge Delivery管道
description: 瞭解如何新增Edge Delivery管道以建置計畫碼並將其部署到生產環境。
index: true
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="早期採用者" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: true
hidefromtoc: true
source-git-commit: 22289138be1fa63caa1beda83e98ffa75dfabc2a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# 新增Edge Delivery管道 {#configure-edge-delivery-pipeline}

瞭解如何設定生產管道以建置計畫碼並將其部署到生產環境。 生產管道會先將計畫碼部署到中繼環境。 在核准後，會將相同的程式碼部署到生產環境。

使用者必須具備&#x200B;**[部署管理員](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)**&#x200B;角色才能設定Edge Delivery管道。

>[!NOTE]
>
>本文所述功能僅可透過早期採用者計畫使用。 如需詳細資訊，以及要註冊為早期採用者，請參閱[自備Git](/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket)。