---
title: 刪除現有安裝的外部依賴項
description: 刪除現有安裝的外部依賴項
feature: Integrations
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
source-git-commit: b71a78696d4b347c97b077d84b455f53a1747a07
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 刪除現有安裝的外部依賴項 {#remove-external-depedencies}

Adobe建議您為Workfront執行現有增強連接器安裝的配置步驟，以刪除對Hoodoo分發點的依賴項。

>[!NOTE]
>
>僅在2022年3月之前為Workfront安裝了增強型連接器時，才執行配置步驟。 從2022年3月起，在Workfront安裝新的增強連接器時，對Hoodoo分發點沒有依賴性。

要刪除外部依賴項：

1. 從父級中刪除以下Hoodoo儲存庫配置 `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. 從 `settings.xml` 檔案，可用於 `./cloudmanager/maven/settings.xml`:

   ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
   ```

1. 執行 [新安裝步驟](workfront-connector-install.md)。
