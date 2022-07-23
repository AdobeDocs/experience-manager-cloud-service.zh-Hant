---
title: 管理SSL證書簡介
description: 瞭解Cloud Manager如何為您提供自助工具來安裝SSL證書。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: f69a26c6156c1f9038d612a00b16cac0e51e17ca
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# 管理SSL證書簡介{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理SSL證書"
>abstract="瞭解Cloud Manager如何為您提供自助服務工具來安裝和管理SSL證書，以保護您的站點的安全。 Cloud Manager使用平台TLS服務來管理客戶擁有並從第三方認證機構獲得的SSL證書和私鑰。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="查看、更新和替換SSL證書"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="檢查SSL證書的狀態"

Cloud Manager為您提供自助服務工具來安裝和管理SSL證書，以保護您的站點供用戶使用。 Cloud Manager使用平台TLS服務來管理客戶擁有的、從第三方認證機構（如Let&#39;s Encrypt）獲取的SSL證書和私鑰。

## 證書簡介 {#certificates}

企業使用SSL證書來保護其網站，並允許其客戶信任他們。 為了使用SSL協定，Web伺服器需要使用SSL證書。

當實體從證書頒發機構請求證書時，CA將完成驗證過程。 這可以從驗證域名控制到收集公司註冊文檔和訂閱者協定。 一旦驗證了實體的資訊，CA將使用CA的私鑰簽名其公鑰。 由於所有主要證書頒發機構在Web瀏覽器中都有根證書，因此將通過 *信任鏈* 而Web瀏覽器會將其識別為可信證書。

>[!IMPORTANT]
>
>雲管理器不提供SSL證書或私鑰。 必須從認證機構(CA)獲得。

## Cloud Manager SSL管理功能 {#features}

Cloud Manager支援以下客戶SSL證書使用選項。

* SSL證書可供多個環境使用。 即可以添加一次，多次使用。
* 每個Cloud Manager環境都可以使用多個證書。
* 私鑰可能頒發多個SSL證書。
* 每個證書通常包含多個域。
* 平台TLS服務基於用於終止的SSL證書和承載該域的CDN服務，將請求路由到客戶的CDN服務。
* AEMas a Cloud Service接受域的通配符SSL證書。

## 建議 {#recommendations}

僅AEMas a Cloud Service `https` 站點。

* 具有多個自定義域的客戶在每次添加域時都不希望上載證書。
* 此類客戶將受益於一個具有多個域的證書。

## 要求 {#requirements}

* AEMas a Cloud Service只接受符合OV（組織驗證）或EV（擴展驗證）策略的證書。
* 任何證書都必須是來自受信任證書頒發機構(CA)的X.509 TLS證書，其中具有匹配的2048位RSA私鑰。
* 不接受DV（域驗證）策略。
* 不接受自簽名證書。

OV和EV證書為用戶提供額外的、經CA驗證的資訊，這些資訊可用於確定網站的所有者、電子郵件的發送者或可執行代碼或PDF文檔的數字簽字人是否可信。 DV證書不允許此類所有權驗證。

## 限制 {#limitations}

在任何給定時間，Cloud Manager將允許最多安裝50個SSL證書。 這些證書可以與您程式中的一個或多個環境相關聯，還可包含任何過期的證書。

如果您已達到限制，請查看您的證書並考慮：

* 正在刪除任何過期的證書。
* 將同一證書中的多個域分組，因為證書可以覆蓋多個域（最多100個SAN）。

## 了解更多 {#learn-more}

具有必要權限的用戶可以使用雲管理器管理程式的SSL證書。 有關使用這些功能的詳細資訊，請參閱以下文檔。

* [添加SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [查看、更新或替換SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [刪除SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
