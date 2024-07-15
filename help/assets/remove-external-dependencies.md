---
title: 移除現有安裝的外部相依性
description: 移除現有安裝的外部相依性
feature: Workfront Integrations and Apps
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
role: Admin
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 17%

---

# 移除現有安裝的外部相依性 {#remove-external-depedencies}

Adobe建議您針對Workfront的現有增強型聯結器安裝執行設定步驟，以移除Hoodoo散發點上的相依性。

>[!NOTE]
>
>僅當您在2022年3月之前安裝適用於Workfront的增強型聯結器時，才執行設定步驟。 自2022年3月起，Workfront新的增強型聯結器安裝不會依賴Hoodoo發佈點。

若要移除外部相依性：

1. 從上層`pom.xml`移除下列Hoodoo存放庫組態：

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. 從`settings.xml`檔案（位於`./cloudmanager/maven/settings.xml`）中移除下列伺服器組態：

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

1. 執行[新安裝步驟](workfront-connector-install.md)。
