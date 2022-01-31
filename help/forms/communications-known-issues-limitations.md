---
title: '已知問題 '
description: 通信最佳做法、已知問題和限制
source-git-commit: 06da7d2a5063e163aa1534bedbc79ae50ef27515
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---


# 常見問題、最佳做法、已知問題和限制 {#best-practices-known-issues-and-limitations}

在開始使用通信API之前，請查看以下已知問題和限制：

## 已知問題

- 在打印選項清單中，只能使用一次特定的渲染類型(PDF、打印)。 例如，不能有兩個PRINT選項，每個選項都指定PCL呈現類型。

- 對於批配置，只有OutputType(PDF、打印)和RenderType（PostScript、PCL、IPL、ZPL等）值組合的一個實例 的子菜單。

## 最佳作法

- Adobe建議在AEM Cloud Service使用的雲區域中托管資料檔案blob容器儲存。

## 常見問題 {#faq}

**是否可以使用監視資料夾或其他儲存機制來儲存輸入和輸出？**

目前，您可以使用MicrosoftAzure儲存來保存輸入資料和生成的文檔。 MicrosoftAzure儲存提供多種選項 [自動化資料移動操作](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)。

**是否包含MicrosoftAzure儲存帳戶與Experience Manager FormsCloud Service許可證？**

MicrosoftAzure儲存帳戶獨立於Experience Manager FormsCloud Service許可證。

**通信API是否在Experience Manager FormsCloud Service伺服器上儲存資料？**

輸入和輸出資料僅保存在MicrosoftAzure儲存上。

**通信API是否僅可用於Experience Manager FormsCloud Service? 是否可以在內部環境中獲得類似的功能？**

您可以使用AEM Forms輸出服務將模板(XFA或PDF)與客戶資料組合，以PDF、PS、PCL和ZPL格式生成文檔。

與現場環境相比，該Cloud Service還提供了自動擴展和成本效益的額外優勢。

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**是否可以同時運行多個批處理操作？**
是，您可以簡單地運行多個批處理工序。 始終對每個操作使用不同的源資料夾和目標資料夾以避免任何衝突。
