---
title: 使用用戶映射工具
description: 使用用戶映射工具
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 3%

---

# 使用用戶映射工具 {#using-user-mapping-tool}

用戶映射工具使用API，它允許它通過電子郵件查找AdobeIdentity Management系統(IMS)用戶並返回其IMS ID。 此API要求用戶為其組織建立客戶端ID、客戶端密鑰和訪問或持有令牌。

## 設定用戶映射工具 {#setting-up-user-mapping}

按照以下步驟設定：

1. 導航到 [Adobe開發人員控制台](https://console.adobe.io) 用你的Adobe ID。
1. 建立新項目或開啟現有項目。
1. 添加API — 按一下 **添加到項目** 選擇 **API**
1. 選擇用戶管理API。  您可能需要獲得權限才能使用此選項。
1. 建立JWT憑據。
1. 生成密鑰對或上載公鑰（rsa不正常）。  有個按鈕， **生成公共/私有密鑰對**&#x200B;這會為你做的。  確保同時保存公鑰和私鑰。
1. 導航至用戶管理API。
1. 通過將私鑰內容貼上到文本框並按一下來生成訪問令牌（或持有者令牌） **生成令牌**。
1. 保存所有此資訊，如 **客戶端ID**。 **客戶端密碼**。 **技術帳戶ID**。 **技術帳戶電子郵件**。 **組織ID**, **訪問令牌** 安全。

## 訪問用戶映射工具的用戶介面 {#user-interface}

用戶映射工具整合到內容傳輸工具中。 您可以從下載內容傳輸工具 [軟體分發門戶](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)。 有關最新版本的詳細資訊，請參閱 [當前發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

1. 選擇Adobe Experience Manager並導航至工具 — > **操作** -> **內容遷移**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. 按一下 **用戶映射** 卡。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. 按一下 **建立用戶映射配置**。

   >[!NOTE]
   >如果跳過此步驟，則在提取階段將跳過用戶和組映射。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   填充中的欄位 **用戶管理API配置**，如下所述。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **組織ID**:輸入要遷移用戶的組織的AdobeIdentity Management系統(IMS)組織ID。

      >[!NOTE]
      >要獲取組織ID，請登錄 [Admin Console](https://adminconsole.adobe.com/) 如果您屬於多個組織，則選擇您的組織（位於右上角）。 組織ID將位於該頁的URL中，格式如下 `xx@AdobeOrg`，其中xx是IMS組織ID。  或者，您可以在 [Adobe開發人員控制台](https://console.adobe.io) 頁面，您可以在其中生成訪問令牌。

   * **客戶端ID**:輸入從「設定」步驟中保存的客戶端ID。

   * **訪問令牌**:輸入從設定步驟中保存的訪問令牌。

      >[!NOTE]
      >訪問令牌每24小時過期一次，需要建立一個新令牌。 要建立新令牌，請返回 [Adobe開發人員控制台](https://console.adobe.io)，選擇項目，按一下 **用戶管理API** 把同一個私鑰貼上到盒子裡。

1. 填充欄位後，按一下 **Test配置** test到用戶管理API服務的連接。 如果連接成功，您將能夠按一下 **保存** 的子菜單。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. 保存配置後，選擇配置，然後按一下 **啟動用戶映射**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. 按一下 **開始** 的子菜單。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   它顯示 **狀態** 如 **正在運行**。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. 用戶映射完成後，按一下 **結果** 的子菜單。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* 完成用戶映射後，可以使用breadcrumb導航回「內容遷移」頁。 用戶映射卡顯示狀態和時間戳。 按一下 **內容傳輸** 建立要運行抽取的遷移集。 請參閱 [運行內容傳輸工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) 的子菜單。


### 繼續用戶映射進程 {#resume-user-mapping-process}

如果由於以下任何原因而停止用戶映射進程：

* 所選用戶 **停止用戶映射**
* 訪問令牌在進程期間過期，或
* 其他原因

   >[!NOTE]
   >進程從進程停止的位置保存。

按照以下步驟繼續「用戶映射」進程：

1. 按一下 **查看日誌** 查看用戶映射日誌以檢查保存的進度。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. 按一下 **啟動用戶映射** 按鈕以從其關閉的位置恢復。

   >[!NOTE]
   >在重新啟動之前確保訪問令牌仍然有效或已刷新。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. 按一下 **開始** 的子菜單。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   用戶映射過程完成後，您將查看 **狀態** 如 **已完成** 特定配置。

   ![影像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
