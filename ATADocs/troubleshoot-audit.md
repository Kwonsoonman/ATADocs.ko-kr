---
title: "ATA 감사 로그 작업 | Microsoft Docs"
description: "이 문서에서는 Windows 이벤트 로그에서 ATA 감사 로그를 사용하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 287bb370f216c2f921eb954dfd4a34ceb8f095c7
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*

# <a name="working-with-ata-audit-logs"></a>ATA 감사 로그 작업

ATA 감사 로그는 ATA 센터 및 ATA 게이트웨이 컴퓨터 둘 다의 Windows 이벤트 로그, **응용 프로그램 및 서비스**와 **Microsoft ATA**에 유지됩니다.

ATA 센터 감사 로그에는 다음이 포함되어 있습니다.
-   의심스러운 활동 정보
-   모니터링 경고(상태 페이지)
-   ATA 콘솔 로그인
-   모든 구성 변경 내용*

ATA 게이트웨이 감사 로그에는 다음이 포함되어 있습니다.
-   게이트웨이 구성 변경 내용* 

모든 ATA 게이트웨이 구성 변경 내용은 ATA 센터에서 구성되지만 여전히 게이트웨이 컴퓨터 자체에서 감사됩니다.

*구성 변경 감사 로그에는 이전 구성과 새 구성이 모두 포함됩니다.


## <a name="see-also"></a>참고 항목
- [의심스러운 활동 작업](working-with-suspicious-activities.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
