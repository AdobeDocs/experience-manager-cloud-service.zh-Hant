---
title: 原始碼儲存庫 — Cloud Services
description: 原始碼儲存庫 — Cloud Services
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# 原始碼存放庫 {#source-code-repository}

Cloud Manager程式將自動配置其自己的Git儲存庫。

用戶若要訪問Cloud Manager Git儲存庫，需要使用帶有命令行工具的Git客戶端、獨立的可視Git客戶端或用戶的IDE（如Eclipse、IntelliJ、NetBeans）。

設定Git客戶端後，您可以從雲管理器UI管理Git儲存庫。 要瞭解如何使用Cloud Manager UI管理Git，請參閱 [訪問Git](/help/implementing/cloud-manager/accessing-git.md)。

要開始開發AEM雲應用程式，必須將應用程式碼的本地副本從Cloud Manager儲存庫簽出到其本地電腦上希望建立儲存庫的位置。

```java
$ git clone {URL}
```

>[!NOTE]
>
>用戶可以簽出其代碼的副本，並在本地代碼儲存庫中進行更改。 準備好後，用戶可以將其代碼更改提交回雲管理器中的遠程代碼儲存庫。
