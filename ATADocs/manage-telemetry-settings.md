---
title: "Advanced Threat Analytics 원격 분석 설정 관리 | Microsoft 관리"
description: "ATA에 의해 수집되는 데이터를 설명하고 데이터 수집을 해제하는 단계를 제공합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2f5db3fad62b0fe2243b5bbd82677426ee6fe90c
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="manage-telemetry-settings"></a>원격 분석 설정 관리
ATA(Advanced Threat Analytics)는 ATA에 대한 익명화된 원격 분석 데이터를 수집하여 HTTPS 연결을 통해 Microsoft 서버로 전송합니다.  이 데이터는 Microsoft에서 이후 버전의 ATA를 개선하는 데 사용됩니다.

## <a name="data-collected"></a>수집되는 데이터
수집되는 익명화된 데이터에는 다음 매개 변수가 포함됩니다.

-   ATA 센터와 ATA 게이트웨이의 성능 카운터

-   사용이 허가된 ATA 복사본의 제품 ID

-   ATA Center 배포 날짜

-   배포된 ATA Gateway 수

-   다음과 같은 익명화된 Active Directory 정보:

    -   사전순으로 정렬할 때 이름이 첫 번째 도메인인 도메인의 도메인 ID

    -   도메인 컨트롤러 수

    -   포트 미러링을 통해 ATA에서 모니터링되는 도메인 컨트롤러 수

    -   사이트 수

    -   컴퓨터 수량

    -   그룹 수

    -   사용자 수

-   의심스러운 활동 - 각 의심스러운 활동에 대해 다음과 같은 익명화된 데이터가 수집됩니다.

    (컴퓨터 이름, 사용자 이름 및 IP 주소는 수집되지 **않음**)

    -   의심스러운 활동 유형

    -   의심스러운 활동 ID

    -   상태

    -   시작 및 종료 시간

    -   제공된 입력

- 각 상태 문제 대해 다음과 같은 익명화된 데이터가 수집됩니다.

    (컴퓨터 이름, 사용자 이름 및 IP 주소는 수집되지 않음)

    -   상태 문제 유형

    -   상태 문제 ID

    -   상태

    -   시작 및 종료 시간

- ATA 콘솔 URL 주소 - ATA 콘솔을 사용할 때 URL 주소(예: ATA 콘솔에서 방문한 페이지).


### <a name="disable-data-collection"></a>데이터 수집 해제
원격 분석 데이터를 수집하여 Microsoft로 전송하는 작업을 중지하려면 다음 단계를 수행합니다.

1.  ATA 콘솔에 로그인하여 도구 모음에 있는 세 점을 클릭하고 **정보**를 선택합니다.

2.  **향후 고객 환경을 개선하기 위해 사용 현황 정보를 보내 주세요.** 확인란의 선택을 취소합니다.

## <a name="see-also"></a>참고 항목
- [이벤트 로그를 사용하여 ATA 문제 해결](troubleshooting-ata-using-logs.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
