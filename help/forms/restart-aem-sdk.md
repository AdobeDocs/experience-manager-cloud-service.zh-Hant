---
title: 如何重新啟動AEM SDK？
description: 重新啟動AEM SDK的最佳做法
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 2%

---

# 重新啟動AEM SDK

如果您藉由停止Java™程式來重新啟動AEM SDK，可能會導致AEM開發環境不一致，並出現下列錯誤：

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![重新啟動 — aem-sdk-error](/help/forms/assets/restart-sdk-error.png)

## 解決方案

若要重新啟動AEM SDK，請移至使用中命令視窗並按`Ctrl + C`命令以重新啟動SDK。

建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK (例如停止Java™程式)，可能會導致AEM開發環境不一致。

## 另請參閱

* [設定AEM Forms的本機開發環境](/help/forms/setup-local-development-environment.md)

