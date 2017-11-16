---
title: "Advanced Threat Analytics 구성 내보내기 및 가져오기 | Microsoft 문서"
description: "ATA 구성을 내보내고 가져오는 방법입니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e1e032adefc650bd4578f29043be313d2c44a866
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="export-and-import-the-ata-configuration"></a>ATA 구성 내보내기 및 가져오기
ATA의 구성은 데이터베이스의 "SystemProfile" 컬렉션에 저장됩니다.
이 컬렉션은 ATA 센터 서비스에 의해 **SystemProfile_*timestamp*.json **파일에 1시간 간격으로 백업됩니다. 최신 10 버전이 저장됩니다. 이 파일은 **Backup**이라는 하위 폴더에 있습니다. 기본 ATA 설치 위치에서는 *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*에서 찾을 수 있습니다. 

**고**: ATA를 대폭 변경할 경우에는 이 파일을 백업하는 것이 좋습니다.

다음 명령을 실행하여 모든 설정을 복원할 수 있습니다.

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>참고 항목
- [ATA 아키텍처](ata-architecture.md)
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

