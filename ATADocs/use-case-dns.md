---
title: "DNS를 사용한 정찰 조사 | Microsoft Docs"
description: "이 문서에서는 DNS를 사용한 정찰을 설명하고 이 위협이 ATA에서 검색될 경우 조사 지침을 제공합니다."
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
ms.openlocfilehash: 5ec554b303a19a6e7b12cd788755604f1aaf43db
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*

# <a name="investigating-reconnaissance-using-dns"></a>DNS를 사용한 정찰 조사

ATA가 네트워크에서 **DNS를 사용한 정찰**을 검색하고 경고할 경우 이 문서의 내용에 따라 경고를 조사하고 문제 해결 방법을 파악합니다.

## <a name="what-is-reconnaissance-using-dns"></a>DNS를 사용한 정찰이란 무엇인가요?

**DNS를 사용한 정찰** 경고는 의심스러운 DNS(Domain Name System) 쿼리가 비정상적인 호스트에서 실행되어 내부 네트워크에 대한 정찰을 수행하고 있음을 나타냅니다.

DNS(Domain Name System)는 호스트 이름 및 도메인 이름 확인을 제공하는 계층적 분산 데이터베이스로 구현된 서비스입니다. DNS 데이터베이스의 이름은 도메인 네임스페이스라는 계층적 트리 구조를 형성합니다.
악의적 사용자에게 DNS는 모든 서버 및 종종 해당 IP 주소에 매핑된 모든 클라이언트 목록을 포함하여 내부 네트워크 매핑을 위한 중요한 정보를 포함합니다. 또한 이 정보는 지정된 네트워크 환경의 설명이 포함된 호스트 이름을 나열하기 때문에 중요한 가치가 있습니다. 악의적 사용자는 이 정보를 검색하여 캠페인 중에 관련 엔터티를 보다 집중적으로 공격할 수 있습니다. [Nmap](https://nmap.org/), [Fierce](https://github.com/mschwager/fierce) 등의 도구와 [Nslookup](https://technet.microsoft.com/library/cc725991(v=ws.11).aspx) 등의 기본 제공 도구는 DNS 정찰을 사용한 호스트 검색 기능을 제공합니다.
내부 호스트에서 DNS 쿼리를 사용한 정찰 검색은 문제의 원인이 되며 기존 호스트 손상, 광범위한 네트워크 손상 또는 내부자 위협 가능성을 나타냅니다.

## <a name="dns-query-types"></a>DNS 쿼리 유형

DNS 프로토콜에는 여러 가지 쿼리 유형이 있습니다. ATA는 AXFR(전송) 요청을 검색하고 발견될 경우 경고를 생성합니다. 이러한 유형의 쿼리는 DNS 서버에서만 수행되어야 합니다.

## <a name="discovering-the-attack"></a>공격 검색

공격자가 DNS를 사용한 정찰을 수행하려고 하면 ATA에서 이를 검색하고 보통 심각도로 표시합니다.

![ATA에서 DNS 정찰 검색](./media/dns-recon.png)
 
ATA는 원본 컴퓨터의 이름과 수행된 실제 DNS 쿼리에 대한 추가 정보를 표시합니다. 예를 들어 동일한 호스트에서 여러 번 시도될 수 있습니다.

## <a name="investigating"></a>조사

DNS를 사용한 정찰을 조사하려면 먼저 쿼리의 원인을 확인해야 합니다. 다음 범주 중 하나로 식별될 수 있습니다. 
-   참 긍정 - 네트워크에 공격자 또는 악성 맬웨어가 있습니다. 네트워크 경계에 도달한 공격자 또는 내부자 위협일 수 있습니다.
-   무해한 참 긍정 - 펜 테스트, 레드 팀 활동, 보안 스캐너, 차세대 방화벽 또는 인가된 활동을 수행하는 IT 관리자에 의해 트리거된 경고일 수 있습니다.
-   가양성 – UDP 포트 53이 ATA 게이트웨이 및 DNS 서버 간에 차단된 경우 등의 잘못된 구성(또는 다른 네트워크 문제)으로 인해 발생하는 경고가 나타날 수 있습니다.

다음 차트를 사용하여 수행해야 하는 조사 단계를 확인할 수 있습니다.

![ATA를 사용한 DNS 정찰 해결](./media/dns-recon-diagram.png)
 
1.  첫 번째 단계는 다음 화면와 그림과 같이 경고가 발생하는 컴퓨터를 식별하는 것입니다.
 
    ![ATA에서 DNS 정찰 의심스러운 활동 보기](./media/dns-recon.png)
2.  이 컴퓨터가 무엇인지 식별합니다. 워크스테이션, 서버, 관리 워크스테이션, 펜 테스트 스테이션 등인가요?
3.  컴퓨터가 DNS 서버이고 영역의 보조 복사본을 요청할 정당한 권한이 있는 경우 거짓 긍정입니다. 거짓 긍정을 찾은 경우 이 컴퓨터에 대해 이 특정 경고가 더 이상 표시되지 않도록 **제외** 옵션을 사용합니다.
4. ATA 게이트웨이와 DNS 서버 간에 UDP 포트 53이 열려 있는지 확인합니다.
4.  컴퓨터가 관리 작업 또는 펜 테스트에 사용되는 경우 무해한 참 긍정이며 관련된 컴퓨터를 예외로 구성할 수도 있습니다.
5.  펜 테스트에 사용되지 않는 경우 컴퓨터에서 AXFR 유형의 DNS 요청을 실행할 수 있는 보안 스캐너 또는 차세대 방화벽을 실행하고 있는지 확인합니다.
6.  마지막으로, 이러한 조건에 부합되지 않을 경우 컴퓨터가 손상되었을 수 있으며 전체 조사를 수행해야 합니다. 
7.  쿼리가 특정 컴퓨터로 격리되고 무해하지 않은 것으로 확인되면 다음 단계를 처리해야 합니다.
    1.  사용 가능한 로그 원본을 검토합니다. 
    2.  호스트 기반 분석을 수행합니다. 
    3.  의심되는 사용자의 활동이 아닌 경우 컴퓨터에서 법정 분석을 수행하여 맬웨어로 손상되었는지 확인해야 합니다.

## <a name="post-investigation"></a>사후 조사

호스트를 손상시키는 데 사용된 맬웨어가 백도어 기능을 가진 트로이 목마를 포함할 수 있습니다. 손상된 호스트에서 성공적인 측면 이동이 확인되면 해당 호스트 및 측면 이동에 포함된 모든 호스트에서 사용된 암호 및 자격 증명 변경을 포함하여 수정 작업을 이러한 호스트까지 확장해야 합니다. 

수정 단계 후 희생자 호스트를 정상으로 확인할 수 없거나 손상의 근본 원인을 식별할 수 없는 경우 중요한 데이터를 백업하고 호스트 컴퓨터를 다시 빌드하는 것이 좋습니다. 또한 네트워크에 다시 배치하기 전에 새로 추가되었거나 다시 빌드된 호스트의 보안을 강화하여 다시 감염되지 않도록 해야 합니다. 

Microsoft 계정 팀을 통해 연락할 수 있는 전문 인시던트 응답 및 복구 팀의 지원을 받아 공격자가 네트워크에 지속성 방법을 배포했는지 검색하는 것이 좋습니다.

## <a name="mitigation"></a>완화 방법

영역 전송을 사용하지 않도록 설정하거나 지정된 IP 주소로만 제한하여 DNS를 사용한 정찰이 발생하지 않도록 내부 DNS 서버의 보안을 설정할 수 있습니다. 영역 전송 제한에 대한 자세한 내용은 [영역 전송 제한](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx)을 참조하세요. [IPsec로 영역 전송의 보안을 설정](https://technet.microsoft.com/library/ee649192(v=ws.10).aspx)하면 제한된 영역 전송을 추가로 잠글 수 있습니다. 영역 전송 수정은 [내부 및 외부 공격으로부터 DNS 서버 보호](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx)를 위해 처리해야 하는 검사 목록의 작업 중 하나입니다.



## <a name="see-also"></a>참고 항목
- [의심스러운 활동 작업](working-with-suspicious-activities.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
