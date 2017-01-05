---
title: "ATA 구성 내보내기 및 가져오기 | Microsoft 문서"
description: "ATA 구성을 내보내고 가져오는 방법입니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/31/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: f0307ae2e8f222e7c58db234b0fb393072ac7444


---

*적용 대상: Advanced Threat Analytics 버전 1.7*



# <a name="export-and-import-the-ata-configuration"></a>ATA 구성 내보내기 및 가져오기
ATA의 구성은 데이터베이스의 "SystemProfile" 컬렉션에 저장됩니다.
이 컬렉션은 ATA 센터 서비스에 의해 "SystemProfile_*timestamp*.json" 파일에 1시간 간격으로 백업됩니다. 최신 10 버전이 저장됩니다.
이 파일은 "Backup"이라는 하위 폴더에 있습니다. 기본 ATA 설치 위치에서는 *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*에서 찾을 수 있습니다. 

**고**: ATA를 대폭 변경할 경우에는 이 파일을 백업하는 것이 좋습니다.

다음 명령을 실행하여 모든 설정을 복원할 수 있습니다.

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>참고 항목
- [ATA 아키텍처](/advanced-threat-analytics/plan-design/ata-architecture)
- [ATA 필수 구성 요소](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jan17_HO1-->


