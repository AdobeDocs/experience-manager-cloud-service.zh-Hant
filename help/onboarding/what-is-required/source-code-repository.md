---
title: 原始碼存放庫 — Cloud Services
description: 原始碼存放庫 — Cloud Services
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# 原始碼存放庫 {#source-code-repository}

Cloud Manager程式會自動布建並隨附自己的Git存放庫。

若要讓使用者存取Cloud Manager Git存放庫，使用者需使用Git用戶端及命令列工具、獨立的視覺化Git用戶端，或使用者的IDE（例如Eclipse、IntelliJ、NetBeans）。

設定Git用戶端後，您就可以從Cloud Manager UI管理Git存放庫。 若要了解如何使用Cloud Manager UI管理Git，請參閱[存取Git](/help/implementing/cloud-manager/accessing-git.md)。

若要開始開發AEM雲端應用程式，必須從Cloud Manager存放庫簽出應用程式程式碼的本機副本，並存放至其本機電腦上要建立存放庫的位置。

```java
$ git clone {URL}
```

>[!NOTE]
>
>使用者可以簽出其程式碼的復本，並在本機程式碼存放庫中進行變更。 準備就緒後，使用者可將其程式碼變更提交回Cloud Manager的遠端程式碼存放庫。
