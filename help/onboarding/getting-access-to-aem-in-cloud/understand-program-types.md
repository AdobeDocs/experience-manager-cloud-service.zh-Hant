---
title: 瞭解方案和方案類型
description: 瞭解方案和方案類型-Cloud Services
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---


# 了解方案和方案類型 {#understanding-programs}

在Cloud Manager中，您的最上層是「租用戶」實體，其中可包含多個「程式」。 每個方案只能包含一個以上的生產環境和多個非生產環境。

下圖顯示Cloud Manager中的實體階層。

![影像](assets/program-types1.png)

## 原始碼存放庫 {#source-code-repository}

Cloud Manager程式會自動布建其專屬的git儲存庫。

若是使用者要存取Cloud Manager Git儲存庫，使用者將需要使用Git用戶端和命令列工具、獨立的視覺化Git用戶端，或使用者的IDE，例如Eclipse、IntelliJ、NetBeans。

設定Git用戶端後，您就可以從Cloud Manager UI管理您的git儲存庫。 要瞭解如何使用Cloud Manager UI管理Git，請參閱[存取Git](/help/implementing/cloud-manager/accessing-git.md)。

要開始開發AEMCloud應用程式，必須從Cloud Manager資料庫將應用程式程式碼簽出至其本機電腦上想要建立資料庫的位置，以製作應用程式程式碼的本機副本。

```java
$ git clone {URL}
```

>[!NOTE]
>使用者可以取出其程式碼的副本，並在本機程式碼儲存庫中進行變更。 當使用者準備就緒後，就可以將其程式碼變更提交回Cloud Manager的遠端程式碼儲存庫。

## 程式類型{#program-types}

用戶可以建立&#x200B;**沙盒**&#x200B;或&#x200B;**生產**&#x200B;程式。

* 建立&#x200B;*生產程式*以在將來的適當時間啟用即時通信。
如需詳細資訊，請參閱[生產程式簡介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md)。


* *沙盒程式*通常是為了提供訓練、執行示範、啟用、POC或說明檔案的目的而建立。 它不是要傳送即時流量，而且會有生產程式不會受到的限制。 它將包含網站和資產，並會自動填入Git分支，其中包含范常式式碼、開發環境和非生產管道。
如需詳細資訊，請參閱[沙盒程式簡介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。

