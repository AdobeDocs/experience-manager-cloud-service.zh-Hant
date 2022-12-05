---
title: 管理 SSL 憑證的簡介
description: 了解 Cloud Manager 如何提供自助服務工具以安裝 SSL 憑證。
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: f69a26c6156c1f9038d612a00b16cac0e51e17ca
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 100%

---


# 管理 SSL 憑證的簡介{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="管理 SSL 憑證"
>abstract="了解 Cloud Manager 如何提供自助服務工具來安裝和管理 SSL 憑證，從而為您的使用者保護您的網站。Cloud Manager 使用平台 TLS 服務來管理客戶擁有並從第三方憑證授權單位獲得的 SSL 憑證和私密金鑰。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html?lang=zh-Hant" text="檢視、更新和取代 SSL 憑證"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="檢查 SSL 憑證狀態"

Cloud Manager 提供自助服務工具來安裝和管理 SSL 憑證，從而為您的使用者保護您的網站。Cloud Manager 使用平台 TLS 服務來管理客戶擁有並從第三方憑證授權單位 (例如 Let’s Encrypt) 獲得的 SSL 憑證和私密金鑰。

## 憑證簡介 {#certificates}

企業使用 SSL 憑證來保護他們的網站，並讓他們的客戶信任他們。為了使用 SSL 協議，Web 伺服器需要使用 SSL 憑證。

當實體向憑證授權單位要求憑證時，CA 會完成驗證計畫。這範圍包含從驗證網域名稱控制到收集公司註冊文件和訂閱協議。實體的資訊獲得驗證後，CA 將使用 CA 的私密金鑰簽署其公開金鑰。由於所有主要的憑證授權單位在 Web 瀏覽器中都有根憑證，因此實體的憑證將透過&#x200B;*信任鏈*&#x200B;連結，且網路瀏覽器會將其識別為受信任的憑證。

>[!IMPORTANT]
>
>Cloud Manager 不提供 SSL 憑證或私密金鑰。這些必須從憑證授權單位 (CA) 獲得。

## Cloud Manager SSL 管理功能 {#features}

Cloud Manager 支援以下客戶 SSL 憑證使用選項。

* 一個 SSL 憑證可以由多個環境使用。即只要新增一次憑證就可多次使用。
* 每個 Cloud Manager 環境都可以使用多個憑證。
* 一個私密金鑰可以發行多個 SSL 憑證。
* 一個憑證通常包含多個網域。
* 平台 TLS 服務根據用於終止的 SSL 憑證和託管該網域的 CDN 服務將要求路由到客戶的 CDN 服務。
* AEM as a Cloud Service 接受網域的萬用字元 SSL 憑證。

## 建議 {#recommendations}

AEM as a Cloud Service 僅支援安全的 `https` 網站。

* 擁有多個自訂網域的客戶不希望每次新增網域時都上傳憑證。
* 這類客戶將能因獲得具有多個網域的憑證而受益。

## 要求 {#requirements}

* AEM as a Cloud Service 僅接受符合 OV (組織驗證) 或 EV (擴展驗證) 原則的憑證。
* 任何憑證都必須是來自受信任憑證授權單位 (CA) 的 X.509 TLS 憑證，並具有相符的 2048 位元 RSA 私密金鑰。
* 不接受 DV (網域驗證) 原則。
* 不接受自我簽署憑證。

OV 和 EV 憑證為使用者提供額外的 CA 驗證資訊，可用於確定網站所有者、電子郵件寄件者或可執行計劃碼或 PDF 文件的數位簽署人是否值得信賴。DV 憑證不允許此類所有權驗證。

## 限制 {#limitations}

在任何指定時間，Cloud Manager 最多允許安裝 50 個 SSL 憑證。這些憑證可以與您的計畫中的一個或多個環境相關聯，並且還包括任何過期的憑證。

如果您已達到限制，請查看您的憑證並考慮：

* 刪除所有過期的憑證。
* 在同一個憑證中對多個網域進行分組，因為一個憑證可以覆蓋多個網域 (最多 100 個 SAN)。

## 了解更多 {#learn-more}

具有必要權限的使用者可以使用 Cloud Manager 來管理計畫的 SSL 憑證。有關使用這些功能的更多詳細資訊，請參閱以下文件。

* [新增 SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [檢視、更新或取代 SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [刪除 SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
