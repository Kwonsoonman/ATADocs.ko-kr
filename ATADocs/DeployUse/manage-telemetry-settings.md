---
title: "원격 분석 설정 관리 | Microsoft Advanced Threat Analytics"
description: "ATA에 의해 수집되는 데이터를 설명하고 데이터 수집을 해제하는 단계를 제공합니다."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: c6b3196f6093b909e8d97f9a9ac230e35807eb72


---

# 원격 분석 설정 관리
ATA(Advanced Threat Analytics)는 ATA에 대한 익명화된 원격 분석 데이터를 수집하여 HTTPS 연결을 통해 Microsoft 서버로 전송합니다.  이 데이터는 Microsoft에서 이후 버전의 ATA를 개선하는 데 사용됩니다.

## 수집되는 데이터
수집되는 익명화된 데이터에는 다음이 포함됩니다.

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

### 데이터 수집 해제
원격 분석 데이터를 수집하여 Microsoft로 전송하는 작업을 중지하려면 다음 단계를 수행합니다.

1.  ATA 콘솔에 로그인하여 도구 모음에 있는 세 점을 클릭하고 **정보**를 선택합니다.

2.  **향후 고객 환경을 개선하기 위해 사용 현황 정보를 보내 주세요.** 확인란의 선택을 취소합니다.

## 참고 항목
- [버전 1.6의 새로운 기능](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


