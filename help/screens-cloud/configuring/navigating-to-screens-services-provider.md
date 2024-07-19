---
title: 瀏覽至 Screens 服務提供者
description: 本頁面說明如何導覽至Screens服務提供者。
exl-id: 9eff6fe8-41d4-4cf3-b412-847850c4e09c
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f91166ca0349636386aa8721ded5b3bbda1cdb51
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 4%

---

# 瀏覽至 Screens 服務提供者 {#setup-screens-services-provider}

## 簡介 {#introduction}

**Screens Services Provider**，可讓內容作者、開發人員和管理員在內容新增至頻道後，管理播放內容的顯示器和播放器。 使用者獲得AEM Cloud Service的存取權後，應該就能登入Screens服務提供者。

本節說明如何設定Screens服務提供者。


## 目標 {#objective}

下節說明如何設定及設定Screens Services Provider。

## 設定Screens服務提供者的步驟 {#screens-services-provider}

請依照下列步驟設定Screens服務提供者：

1. 從[這裡](https://experience.adobe.com/screens)瀏覽至Screens服務提供者。

   >[!CAUTION]
   >如果您可以存取多個組織，請確保您已登入正確的組織。 若要變更您的組織，請按一下畫面右上角的「組織」名稱，然後選擇您需要存取的所需組織。

1. 按一下「專案」 （左上角）旁的齒輪圖示

   ![影像](/help/screens-cloud/assets/configure/configure-screens0.png)

1. 在「編輯設定」對話方塊中輸入下列詳細資料。
   * **Publish Url** - AEM發佈URL （例如，`https://publish-p12345-e12345.adobeaemcloud.com`）
   * **作者URL** - AEM作者URL （例如，`https://author-p12345-e12345.adobeaemcloud.com`）

   >[!NOTE]
   >在Screens服務提供者底下設定AEM之前，請確定您建立和發佈至少一個AEM畫面頻道。 若要建立頻道，請導覽至內容提供者上的/screens.html 。

   ![影像](/help/screens-cloud/assets/configure/configure-screens4.png)

1. 按一下&#x200B;**儲存**&#x200B;以連線至Screens內容提供者。

1. 如果您已透過Cloud Manager的IP允許清單功能將AEM發佈執行個體設定為僅允許存取受信任的IP位址，則您必須在設定對話方塊中設定具有索引鍵值的標頭，如下所示。
需要列入白名單的IP也需要移至設定檔，並且需要從Cloud Manager設定中[取消套用](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list)。

   ![影像](/help/screens-cloud/assets/configure/configure-screens20.png)

需要在AEM CDN設定中設定相同的金鑰。  建議不要直接將標頭值放入GITHub中，並使用[機密參考](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-credentials-authentication#rotating-secrets)。
以下提供範例[CDN設定](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf)：

    kind： &quot;CDN&quot;
    version： &quot;1&quot;
    metadata：
    envTypes： [&quot;dev&quot;， &quot;stage&quot;， &quot;prod&quot;]
    資料：
    trafficFilters：
    規則：
     — 名稱： &quot;block-request-from-not-allowed-ips&quot;
    when：
    allOf：
    - reqProperty： clientIp
    notIn： [&quot;101.41.112.0/24&quot;]
    - reqProperty： tier： tier
    equequequals： publish
     4}操作：塊
     — 名稱：「allow-requests-with-header」
    時間：
    allOf：
    - reqProperty： tier
    equals： publish
    - reqProperty： path
    equals： /screens/channels.json
    - reqHeader： x-screens-allowlist-key
    equals： ${\
    {CDN_HEADER_KEY}
    操作：
    型別： allow

1. 從左側導覽列中選取&#x200B;**管道**，然後按一下內容提供者中的&#x200B;**開啟**。

   ![影像](/help/screens-cloud/assets/configure/configure-screens1.png)

1. Screens內容提供者會在另一個標籤中開啟，讓您建立內容。

   ![影像](/help/screens-cloud/assets/configure/configure-screens2.png)

## 下一步 {#whats-next}

瞭解如何設定Screens服務提供者後，請瀏覽至[使用Screens內容提供者](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html#screens-content-provider)以取得詳細資訊。
