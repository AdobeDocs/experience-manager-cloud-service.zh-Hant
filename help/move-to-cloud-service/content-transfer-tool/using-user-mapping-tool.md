---
title: 使用用戶映射工具
description: 使用用戶映射工具
translation-type: tm+mt
source-git-commit: 664c278494a5ac88362b994946060ab3baa846d8
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# 使用用戶映射工具{#user-mapping-tool}

## 概覽 {#overview}

在AEM的雲端服務轉型歷程中，您需要將使用者和群組從您現有的AEM系統移至AEM做為雲端服務。 這是由內容傳輸工具完成。

AEM雲端服務的重大變更，是完全整合使用Adobe ID來存取作者層。  這需要使用Adobe Admin Console來管理使用者和使用者群組。 使用者設定檔資訊會集中在Adobe Identity Management System(IMS)中，該系統可跨所有Adobe雲端應用程式提供單一登入。 如需詳細資訊，請參閱「身分識別管理」。 由於這項變更，現有的使用者和群組必須對應至其IMS ID，以避免在雲端服務作者實例上重複使用者和群組。

## 重要注意事項{#important-considerations}

有一些例外情況需要考慮。 將記錄下列特定案例，且不會映射相關的使用者或群組：

1. 如果用戶在其jcr節點的`profile/email`欄位中沒有電子郵件地址。

1. 如果在IMS系統上找不到使用之組織ID的指定電子郵件（或是由於其他原因無法擷取IMS ID）。

1. 如果使用者目前已停用，則會視為未停用的使用者。  它會以正常方式進行映射和移轉，並在雲端例項上仍會停用。

## 使用用戶映射工具{#using-user-mapping-tool}

使用者對應工具使用API，可讓它透過電子郵件查閱IMS使用者並傳回其IMS ID。 此API要求使用者為其組織建立用戶端ID、用戶端密碼和存取Token/Bearer Token。

請依照下列步驟設定：

1. 使用您的Adobe ID導覽至[Adobe Developer Console](https://console.adobe.io)。
1. 建立新專案或開啟現有專案
1. 新增API
1. 選擇使用者管理API
1. 建立JWT憑據
1. 產生金鑰對，或上傳公開金鑰（rsa不行）
1. 產生存取Token（或JWT Token或承載Token）。
1. 將所有這些資訊（用戶端ID、用戶端密碼、技術帳戶ID、技術帳戶電子郵件、組織ID、存取Token）儲存在安全的位置。