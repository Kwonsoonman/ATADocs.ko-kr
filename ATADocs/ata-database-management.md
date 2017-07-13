---
title: "Advanced Threat Analytics 데이터베이스 관리 | Microsoft 문서"
description: "ATA 데이터베이스를 이동, 백업 또는 복원할 수 있는 절차를 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4fe667574ea011c032bacd8f5bce4b07c2c46602
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/30/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# ATA 데이터베이스 관리
<a id="ata-database-management" class="xliff"></a>
ATA 데이터베이스를 이동, 백업 또는 복원해야 하는 경우에는 아래에 나와 있는 MongoDB 사용 절차를 수행하세요.

## ATA 데이터베이스 백업
<a id="backing-up-the-ata-database" class="xliff"></a>
[관련 MongoDB 설명서](http://docs.mongodb.org/manual/administration/backup/)를 참조하세요.

## ATA 데이터베이스 복원
<a id="restoring-the-ata-database" class="xliff"></a>
[관련 MongoDB 설명서](http://docs.mongodb.org/manual/administration/backup/)를 참조하세요.

## 다른 드라이브로 ATA 데이터베이스 이동
<a id="moving-the-ata-database-to-another-drive" class="xliff"></a>

1.  **Microsoft Advanced Threat Analytics 센터** 서비스를 중지합니다.
> [!Important] 
> 다음 단계로 넘어가기 전에 ATA 센터 서비스가 중지되었는지 확인합니다.

2.  **MongoDB** 서비스를 중지합니다.

3.  Mongo 구성 파일(기본 위치: C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg)을 엽니다.

    `storage: dbPath` 매개 변수를 찾습니다.

4.  `dbPath` 매개 변수에 나와 있는 폴더를 새 위치로 이동합니다.

5.  Mongo 구성 파일 내의 `dbPath` 매개 변수를 새 폴더 경로로 변경하고 파일을 저장한 후에 닫습니다.

    ![MongoDB 구성 이미지 수정](media/ATA-mongoDB-moveDB.png)

6.  **MongoDB** 서비스를 시작합니다.

7. **Microsoft Advanced Threat Analytics 센터** 서비스를 시작합니다.

## 참고 항목
<a id="see-also" class="xliff"></a>
- [ATA 아키텍처](ata-architecture.md)
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

