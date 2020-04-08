---
title: 原始碼儲存庫——雲端服務
description: 原始碼儲存庫——雲端服務
translation-type: tm+mt
source-git-commit: 114bc678fc1c6e3570d6d2a29bc034feb68aa56d

---


# 原始碼存放庫 {#source-code-repository}

Cloud Manager程式會自動布建其專屬的git儲存庫。

若是使用者要存取Cloud Manager Git儲存庫，使用者將需要使用Git用戶端和命令列工具、獨立的視覺化Git用戶端，或使用者的IDE，例如Eclipse、IntelliJ、NetBeans。

設定Git用戶端後，您就可以從Cloud Manager UI管理您的git儲存庫。 如要瞭解如何使用Cloud Manager UI管理Git，請參閱「存 [取Git](/help/implementing/cloud-manager/accessing-git.md)」。

若要開始開發AEM Cloud應用程式，必須從Cloud Manager儲存庫將應用程式程式碼簽出至其本機電腦上想要建立儲存庫的位置，以製作應用程式程式碼的本機副本。

```java
$ git clone {URL}
```

>[!NOTE]
>
> 使用者可以取出其程式碼的副本，並在本機程式碼儲存庫中進行變更。 當使用者準備就緒後，就可以將其程式碼變更提交回Cloud Manager的遠端程式碼儲存庫。
