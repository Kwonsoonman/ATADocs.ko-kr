---
title: "ATA 버전 1.8의 새로운 기능 | Microsoft Docs"
description: "알려진 문제와 함께 ATA 버전 1.8의 새로운 기능을 나열합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: f2a4ed151db38497a6cec977f1090faf2eb4133e
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2017
---
# ATA 버전 1.8의 새로운 기능
<a id="whats-new-in-ata-version-18" class="xliff"></a>
이 릴리스 정보에서는 이 Advanced Threat Analytics 버전의 업데이트, 새로운 기능, 버그 수정 및 알려진 문제에 대한 정보를 제공합니다.



## 새롭거나 업데이트된 검색 기능
<a id="new--updated-detections" class="xliff"></a>

- 비정상적인 프로토콜 구현이 WannaCry 맬웨어를 검색하도록 향상되었습니다.

- 새 기능! **중요한 그룹의 비정상적인 수정** – 권한 상승 단계의 일부로 공격자가 중요한 리소스에 대한 액세스 권한을 얻기 위해 높은 권한을 가진 그룹을 수정합니다. 이제 ATA가 관리자 권한 그룹에 비정상적인 변경이 있을 경우 이를 검색합니다.
- 새 기능! **의심스러운 인증 실패**(동작 무차별 암호 대입(Brute force)) – 공격자가 자격 증명에 무차별 암호 대입(Brute force)을 사용하여 계정을 손상하려고 합니다. 이제 비정상적인 인증 실패 동작이 검색되면 ATA에서 경고가 발생합니다.   

- **원격 실행 시도 - WMI 실행** - 공격자는 도메인 컨트롤러에서 원격으로 코드를 실행하여 네트워크를 제어하려고 시도할 수 있습니다. ATA에서 원격으로 코드를 실행하는 WMI 메서드 검색을 포함하도록 원격 실행 검색 기능이 향상되었습니다.

- 디렉터리 서비스 쿼리를 사용한 정찰 – 이 검색은 하나의 중요한 엔터티에 대한 쿼리를 catch하고 이전 버전에서 생성된 거짓 긍정 수를 줄일 수 있도록 향상되었습니다. 버전 1.7에서 이 기능을 사용하지 않도록 설정한 경우 버전 1.8을 설치하면 이제 자동으로 사용됩니다.

- Kerberos 골든 티켓 활동 - ATA 1.8에는 골든 티켓 공격을 검색하는 추가 기술이 포함되어 있습니다.
    - 이제 ATA가 골든 티켓 수명이 만료된 의심스러운 활동을 검색합니다. Kerberos 티켓이 허용된 수명보다 오래 사용되면 ATA는 골든 티켓이 생성되었을 가능성이 있는 의심스러운 활동으로 검색합니다.
- 알려진 거짓 긍정을 제거하기 위해 다음 검색이 향상되었습니다.  
    - 권한 상승 검색(위조된 PAC) 
    - 암호화 다운그레이드 활동(스켈레톤 키)
    - 비정상적인 프로토콜 구현
    - 손상된 신뢰

## 의심스러운 활동의 향상된 심사
<a id="improved-triage-of-suspicious-activities" class="xliff"></a>

-   새 기능! ATA 1.8에서는 심사 프로세스 중 의심스러운 활동에 대해 다음과 같은 작업을 실행할 수 있습니다. 
    - **엔터티 제외** - ATA에서 원격 코드를 실행하는 관리자, 보안 스캐너 검색 등 무해한 참 긍정을 검색할 때 경고하지 않도록 향후 의심스러운 활동 발생에서 엔터티를 제외합니다.
    - **반복 표시 안 함** - 의심스러운 활동에 대한 경고가 반복해서 표시되지 않도록 합니다.
    - **의심스러운 활동 삭제** - 공격 타임라인에서 의심스러운 활동을 삭제합니다.
-   이제 의심스러운 활동 경고에 대한 후속 작업 프로세스가 더 효율적입니다. 의심스러운 활동 타임라인이 다시 설계되었습니다. ATA 1.8에서는 단일 화면에 더 많은 의심스러운 활동을 표시하고, 심사 및 조사를 위해 더 나은 정보를 포함할 수 있습니다. 

## 조사에 도움이 되는 새로운 보고서
<a id="new-reports-to-help-you-investigate" class="xliff"></a> 
-   새 기능! 의심스러운 활동, 상태 문제 등을 포함하여 ATA에서 요약된 모든 데이터를 볼 수 있도록 **요약 보고서**가 추가되었습니다. 반복해서 자동으로 생성되는 사용자 지정 보고서를 정의할 수도 있습니다.
-   새 기능! 특정 기간 동안 중요한 그룹에서 변경된 모든 내용을 볼 수 있도록 **중요한 그룹 보고서**가 추가되었습니다.


## 인프라 향상
<a id="infrastructure-improvements" class="xliff"></a>

-   ATA 센터 성능이 향상되었습니다. ATA 1.8에서는 ATA 센터가 초당 1M 이상의 패킷을 처리할 수 있습니다.
-   이제 ATA 경량 게이트웨이가 이벤트 전달을 구성하지 않고도 로컬에서 이벤트를 읽을 수 있습니다.
-   접근성 확장 - 이제 ATA에서 Microsoft와 협력하여 접근성이 높은 제품을 제공합니다. 
-   이제 모니터링 경고 및 의심스러운 활동에 대해 별도로 메일을 구성할 수 있습니다.

## 향상된 보안 기능
<a id="security-improvements" class="xliff"></a>

-   새 기능! **ATA 관리에 대한 Single Sign-On**. ATA는 Windows 인증과 통합된 Single Sign-On을 지원합니다. 컴퓨터에 이미 로그온되어 있으면 ATA는 해당 토큰을 사용하여 ATA 콘솔에 로그인합니다. 스마트 카드를 사용하여 로그인할 수도 있습니다. ATA 게이트웨이 및 ATA 경량 게이트웨이에 대한 자동 설치 스크립트에서 이제 자격 증명을 제공할 필요 없이 로그온한 사용자의 컨텍스트를 사용합니다.
-   로컬 시스템 권한이 ATA 게이트웨이 프로세스에서 제거되었으므로 이제 가상 계정(독립 실행형 ATA 게이트웨이에서만 사용 가능), 관리 서비스 계정 및 그룹 관리 서비스 계정을 사용하여 ATA 게이트웨이 프로세스를 실행할 수 있습니다.   
-   ATA 센터 및 게이트웨이에 대한 감사 로그가 추가되었으며, 이제 모든 작업이 Windows 이벤트 로그에 기록됩니다.
-   ATA 센터에 대한 KSP 인증서 지원이 추가되었습니다.




## 참고 항목
<a id="see-also" class="xliff"></a>
[ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[버전 1.8로 ATA 업데이트 - 마이그레이션 가이드](ata-update-1.8-migration-guide.md)
