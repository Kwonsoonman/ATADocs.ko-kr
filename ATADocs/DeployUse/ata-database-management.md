---
title: "ATA 데이터베이스 관리 | Microsoft ATA"
description: "ATA 데이터베이스를 이동, 백업 또는 복원할 수 있는 절차를 설명합니다."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5cd030f3b952d08c6617a6cda121c344a9c36f51
ms.openlocfilehash: b4e68e9e8dbd94075a34a8e3e8f42d4f534caf50


---

*적용 대상: Advanced Threat Analytics 버전 1.7*



# ATA 데이터베이스 관리
ATA 데이터베이스를 이동, 백업 또는 복원해야 하는 경우에는 아래에 나와 있는 MongoDB 사용 절차를 수행하세요.

## ATA 데이터베이스 백업
[관련 MongoDB 설명서](http://docs.mongodb.org/manual/administration/backup/)를 참조하세요.

## ATA 데이터베이스 복원
[관련 MongoDB 설명서](http://docs.mongodb.org/manual/administration/backup/)를 참조하세요.

## 다른 드라이브로 ATA 데이터베이스 이동

1.  **Microsoft Advanced Threat Analytics 센터** 서비스를 중지합니다.

2.  **MongoDB** 서비스를 중지합니다.

3.  Mongo 구성 파일(기본 위치: C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg)을 엽니다.

    매개 변수 찾기 `storage: dbPath`

4.  `dbPath` 매개 변수에 나와 있는 폴더를 새 위치로 이동합니다.

5.  Mongo 구성 파일 내의 `dbPath` 매개 변수를 새 폴더 경로로 변경하고 파일을 저장한 후에 닫습니다.

    ![MongoDB 구성 이미지 수정](media/ATA-mongoDB-moveDB.png)

6.  **MongoDB** 서비스를 시작합니다.

7. **Microsoft Advanced Threat Analytics 센터** 서비스를 시작합니다.

## ATA 구성 파일
ATA의 구성은 데이터베이스의 "SystemProfile" 컬렉션에 저장됩니다.
이 컬렉션은 ATA 센터 서비스에 의해 "SystemProfile_*timestamp*.json" 파일에 1시간 간격으로 백업됩니다. 최신 10 버전이 저장됩니다.
이 파일은 "Backup"이라는 하위 폴더에 있습니다. 기본 ATA 설치 위치에서는 *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*에서 찾을 수 있습니다. 

**고**: ATA를 대폭 변경할 경우에는 이 파일을 백업하는 것이 좋습니다.

다음 명령을 실행하여 모든 설정을 복원할 수 있습니다.

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## 참고 항목
- [ATA 아키텍처](/advanced-threat-analytics/plan-design/ata-architecture)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Aug16_HO5-->


