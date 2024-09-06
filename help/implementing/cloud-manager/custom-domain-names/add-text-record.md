---
title: 新增 TXT 記錄
description: 瞭解如何新增TXT記錄以驗證您對用於Cloud Manager的自訂網域的擁有權。
exl-id: d441de29-af41-4d3e-9155-531af9702841
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5d6d3374f2dd95728b2d3ed0cf6fab4092f73568
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 28%

---


# 新增 TXT 記錄 {#adding-txt}

瞭解如何新增TXT記錄以驗證您對用於Cloud Manager的自訂網域的擁有權。

## 什麼是TXT記錄？ {#what-is}

文字記錄（也稱為TXT記錄）是網域名稱系統(DNS)中的資源記錄型別。 它提供將任意文字與主機名稱關聯的能力，例如有關主機名稱的可讀取資訊，例如伺服器或網路資訊。

Cloud Manager使用特定TXT記錄來授權要在CDN服務中託管的網域。 您必須在授權了Cloud Manager使用自訂網域部署CDN服務並將其與後端服務關聯的區域中建立DNS TXT記錄。 此關聯完全在您的控制之下，並授權 Cloud Manager 將內容從服務提供給網域。這種授權可以被授予也可以被撤銷。TXT記錄特定於網域和Cloud Manager環境。

## 要求 {#requirements}

在新增 TXT 記錄之前，您必須滿足這些要求。

* 如果您還不知道您的網域名稱主機服務商或註冊商，則必須確定它。
* 您必須能夠編輯組織網域的DNS記錄，或聯絡可以編輯的適當人員。
* 您必須先新增自訂網域名稱，如檔案[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)中所述。

## 新增TXT記錄以進行驗證 {#verification}

新增TXT記錄以作為驗證要與Cloud Manager一起使用的自訂網域名稱的一部分。

1. 您必須先新增自訂網域名稱，如檔案[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)中所述。

1. 在&#x200B;**新增網域名稱**&#x200B;對話方塊的&#x200B;**驗證**&#x200B;索引標籤上，Cloud Manager會顯示用於驗證的名稱和TXT值。 複製此值。

   ![網域名稱識別](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

1. 登入您的網域主機並找到DNS記錄區段。

1. 新增`_aemverification.[yourdomainname]`作為值的&#x200B;**Name**，並新增TXT值，就像它在&#x200B;**新增網域名稱**&#x200B;對話方塊中所顯示的一樣。

   * 請參閱下節](#examples)中的[範例。

1. 將TXT記錄儲存至您的網域主機。

## TXT記錄範例 {#examples}

| 網域 | 名稱 | TXT 數值 |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | 複製 Cloud Manager UI 中顯示的整個值。這是特定於網域和環境的。例如：<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | 複製 Cloud Manager UI 中顯示的整個值。這是特定於網域和環境的。例如：<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

## 驗證TXT記錄 {#verify}

完成後，可執行下列指令來驗證結果。

```shell
dig _aemverification.[yourdomainname] -t txt
```

預期結果應顯示Cloud Manager UI之&#x200B;**新增網域名稱**&#x200B;對話方塊的&#x200B;**驗證**&#x200B;索引標籤上提供的TXT值。

例如，如果您的網域是 `example.com`，然後執行：

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>有數個[DNS查詢工具](https://www.ultratools.com/tools/dnsLookup)可供使用。 Google DoH 可用於查找 TXT 記錄項目並識別 TXT 記錄是否遺失或錯誤。

>[!NOTE]
>
>由於 DNS 傳播延遲，DNS 驗證可能需要幾個小時才能完成。
>
>Cloud Manager 將驗證所有權並更新可在域設定表中看到的狀態。如需更多詳細資訊，請參閱[檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。

## 後續步驟 {#next-steps}

現在您已建立TXT專案，可以驗證網域名稱狀態了。 繼續檔案[檢查網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)以繼續設定您的自訂網域名稱。

>[!TIP]
>
>TXT專案和CNAME或A記錄可以同時設定在控管的DNS伺服器上，因此可節省時間。
>
>若要這麼做，請先檢閱設定自訂網域名稱的整個程式，如檔案[自訂網域名稱簡介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)中所詳述，特別記下檔案[help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)，並適當地更新您的DNS設定。