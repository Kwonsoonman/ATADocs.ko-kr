---
# required metadata

title: ATA 아키텍처 | Microsoft Advanced Threat Analytics
description: Microsoft Advanced Threat Analytics(ATA)의 아키텍처에 대해 설명합니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 아키텍처
아래 다이어그램에는 Advanced Threat Analytics 아키텍처가 자세히 나와 있습니다.

![ATA 아키텍처 토폴로지 다이어그램](media/ATA-architecture-topology.jpg)

ATA에는 두 가지 주요 구성 요소인 ATA 게이트웨이와 ATA 센터가 포함되어 있습니다.

이러한 구성 요소는 도메인 컨트롤러에서 보내고 받는 네트워크 트래픽을 미러링하고, 도메인 컨트롤러나 SIEM 서버에서 직접 전달되는 Windows 이벤트를 확인하여 데이터에서 공격과 위협을 분석하는 방식으로 기존 네트워크에 연결합니다.

이 섹션에서는 네트워크 및 이벤트 캡처 흐름에 대해 설명하고, ATA 게이트웨이 및 ATA 센터의 기본 구성 요소와 해당 기능에 대해 자세히 살펴봅니다.

![ATA 트래픽 흐름 다이어그램](media/ATA-traffic-flow.jpg)

## ATA 구성 요소
ATA는 다음 구성 요소로 이루어져 있습니다.

-   하나 이상의 ATA 게이트웨이

-   ATA 센터 하나

## ATA 게이트웨이
**ATA 게이트웨이**는 다음 기능을 수행합니다.

-   포트 미러링을 통해 도메인 컨트롤러 네트워크 트래픽 캡처 및 검사

-   Windows 이벤트 전달 기능을 통해 SIEM 또는 Syslog 서버나 도메인 컨트롤러에서 Windows 이벤트 수신

-   Active Directory 도메인에서 사용자 및 컴퓨터에 대한 데이터 검색

-   네트워크 엔터티(사용자, 그룹 및 컴퓨터) 확인 수행

-   ATA 센터에 관련 데이터 전송

-   단일 ATA 게이트웨이에서 여러 도메인 컨트롤러 모니터링

ATA 게이트웨이는 네트워크에서 미러링된 네트워크 트래픽과 Windows 이벤트를 수신하여 다음과 같은 기본 구성 요소에서 처리합니다.

|||
|-|-|
|네트워크 수신기|네트워크 수신기는 네트워크 트래픽 캡처 및 트래픽 구문 분석을 수행합니다. 이러한 작업에서는 CPU를 많이 사용하므로 ATA 게이트웨이를 계획할 때는 [ATA 필수 구성 요소](/advanced-threat-analytics/PlanDesign/ata-prerequisites)를 확인하는 것이 특히 중요합니다.|
|이벤트 수신기|이벤트 수신기는 네트워크의 SIEM 서버에서 전달되는 Windows 이벤트를 캡처하고 구문 분석합니다.|
|Windows 이벤트 로그 판독기|Windows 이벤트 로그 판독기는 도메인 컨트롤러에서 ATA 게이트웨이의 Windows 이벤트 로그로 전달된 Windows 이벤트를 읽고 구문 분석합니다.|
|네트워크 활동 변환기 | 구문 분석된 트래픽을 ATA의 논리적 트래픽 표현(NetworkActivity)으로 변환합니다.
|엔터티 확인자|엔터티 확인자는 구문 분석된 데이터(네트워크 트래픽 및 이벤트)를 가져와 Active Directory에서 확인하여 계정 및 ID 정보를 찾은 다음 구문 분석된 데이터에서 찾은 IP 주소와의 일치 여부를 확인합니다.  또한 패킷 헤더를 효율적으로 검사하고, 인증 패킷에서 컴퓨터 이름/속성/ID를 구문 분석할 수 있도록 설정하며, 구문 분석된 데이터를 실제 패킷의 데이터와 결합합니다.|
|엔터티 발신자|엔터티 발신자는 구문 분석되어 일치 여부가 확인된 데이터를 ATA 센터로 보냅니다.|
네트워크에서 배포할 ATA 게이트웨이의 수를 결정할 때는 다음 사항을 고려하세요.

-   Active Directory 포리스트 및 도메인

    ATA 게이트웨이는 Active Directory 포리스트 하나에서 여러 도메인의 트래픽을 모니터링할 수 있습니다.   여러 Active Directory 포리스트를 모니터링하려면 별도의 ATA를 배포해야 합니다. 서로 다른 여러 포리스트의 도메인 컨트롤러에서 네트워크 트래픽을 모니터링하도록 ATA 게이트웨이를 구성해서는 안 됩니다.

-   포트 미러링

    포트 미러링을 고려하는 경우 데이터 센터/지역당 ATA 게이트웨이를 하나 이상 배포해야 할 가능성이 높습니다.

-   Capacity

    각 ATA 게이트웨이는 초당 일정량의 트래픽을 구문 분석하고 보낼 수 있습니다. 모니터링 중인 도메인 컨트롤러에서 ATA 게이트웨이가 처리할 수 있는 것보다 많은 트래픽을 보내고 받는 경우에는 트래픽 양에 따라 ATA 게이트웨이를 더 추가해야 합니다. 자세한 내용은 [ATA 용량 계획](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)을 참조하세요.

## ATA 센터
**ATA 센터**는 다음 기능을 수행합니다.

-   ATA 게이트웨이 구성 설정 관리

-   ATA 게이트웨이에서 데이터 수신

-   의심스러운 활동 검색

-   다양한 동작 기계 학습 엔진 실행

-   ATA 콘솔 실행

-   선택 사항: 의심스러운 활동이 검색되면 전자 메일과 이벤트를 보내도록 ATA 센터 구성 가능

ATA 센터는 ATA 게이트웨이에서 구문 분석된 트래픽을 받고 프로파일링을 수행합니다. 또한 비정상 상태를 검색하고 의심스러운 활동을 경고할 수 있도록 결정적 검색과 기계 학습 및 동작 알고리즘을 실행하여 네트워크 관련 정보를 학습합니다.

|||
|-|-|
|엔터티 수신기|모든 ATA 게이트웨이에서 엔터티 배치를 받습니다.|
|네트워크 활동 처리기|받은 각 배치 내의 모든 네트워크 활동을 처리합니다. 예를 들어 서로 다를 수 있는 컴퓨터에서 수행한 여러 Kerberos 단계가 일치하는지를 확인합니다.|
|엔터티 프로파일러|트래픽과 이벤트에 따라 모든 고유 엔터티를 프로파일링합니다. 예를 들어 ATA는 엔터티 프로파일러에서 각 사용자 프로필에 대해 로그온한 컴퓨터 목록을 업데이트합니다.|
|ATA 센터 데이터베이스 클라이언트 |네트워크 활동과 이벤트를 데이터베이스에 기록하는 프로세스를 관리합니다. |
|데이터베이스|ATA는 MongoDB를 사용하여 다음과 같은 시스템의 모든 데이터를 저장합니다.<br /><br />-   네트워크 활동<br />-   이벤트<br />-   고유 엔터티<br />-   의심스러운 활동<br />-   ATA 구성|
|검색 엔진|검색 엔진은 기계 학습 알고리즘과 결정적 규칙을 사용하여 네트워크에서 의심스러운 활동과 비정상적인 사용자 동작을 찾습니다.|
|ATA 콘솔|ATA 콘솔은 ATA를 구성하고 네트워크에서 ATA가 검색한 의심스러운 활동을 모니터링하는 데 사용됩니다. ATA 콘솔은 ATA 센터 서비스 실행 여부와 관계없이 실행됩니다. 즉, 서비스가 중지되어도 ATA 콘솔은 데이터베이스와 통신할 수 있으면 실행됩니다.|
네트워크에서 배포할 ATA 센터의 수를 결정할 때는 다음 사항을 고려하세요.

-   각 ATA 센터는 Active Directory 포리스트 하나를 모니터링할 수 있습니다. Active Directory 포리스트가 둘 이상인 경우에는 Active Directory 포리스트당 최소 하나의 ATA 센터가 필요합니다.

    대규모 Active Directory 배포에서는 ATA 센터 하나가 모든 도메인 컨트롤러의 트래픽을 모두 처리하지 못할 수도 있습니다. 이 경우에는 여러 ATA 센터가 필요하며, ATA 검색 효율성이 낮아집니다. ATA 센터의 수는 [ATA 용량 계획](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)에 따라 결정해야 합니다.

## 네트워크 구성 요소
기존 네트워크를 거의 변경하지 않고도 ATA를 사용할 수 있습니다. 그러나 다음 사항은 확인해야 합니다.

### 포트 미러링
모니터링 중인 Active Directory 포리스트의 모든 도메인 컨트롤러에 대해 포트 미러링을 사용하도록 설정해야 ATA가 작동합니다. 일부 도메인 컨트롤러에서 ATA에 대해 포트 미러링을 사용하도록 설정해도 ATA가 작동하기는 하지만 검색 효율성은 낮아집니다.

포트 미러링은 도메인 컨트롤러에서 ATA 게이트웨이 방향으로 설정합니다. 이렇게 하면 ATA 게이트웨이에 대한 모든 도메인 컨트롤러 네트워크 트래픽이 미러링되며 해당 트래픽 중 극히 일부분만이 분석을 위해 압축되어 ATA 센터로 전송됩니다.

도메인 컨트롤러와 ATA 게이트웨이는 실제 하드웨어일 수도 있고 가상 하드웨어일 수도 있습니다. 자세한 내용은 [포트 미러링 구성](/advanced-threat-analytics/PlanDesign/configure-port-mirroring)을 참조하세요.

### 이벤트
ATA의 Pass-the-Hash 공격 검색 기능을 개선하려면 ATA에서 Windows 이벤트 로그 ID 4776을 사용해야 합니다. 두 가지 방법으로 ATA 게이트웨이에 이 ID를 전달할 수 있습니다. 그중 하나는 ATA 게이트웨이가 SIEM 이벤트를 수신하도록 구성하는 것이고, 다른 하나는 Windows 이벤트 전달을 사용하는 것입니다.

-   SIEM 이벤트를 수신하도록 ATA 게이트웨이 구성

    특정 Windows 이벤트를 ATA로 전달하도록 SIEM을 구성합니다. ATA는 다수의 SIEM 공급업체를 지원합니다. 자세한 내용은 [이벤트 수집 구성](/advanced-threat-analytics/PlanDesign/configure-event-collection)을 참조하세요.

-   Windows 이벤트 전달 구성

    ATA가 이벤트를 받을 수 있도록 하는 또 다른 방법은, Windows 이벤트 4776을 ATA 게이트웨이로 전달하도록 도메인 컨트롤러를 구성하는 것입니다. SIEM이 없거나 SIEM이 현재 ATA에서 지원되지 않는 경우 이 방법을 사용하면 특히 유용합니다. ATA의 Windows 이벤트 전달 기능에 대한 자세한 내용은 [Windows 이벤트 전달 구성](/advanced-threat-analytics/PlanDesign/configure-event-collection#ATA_event_WEF)을 참조하세요.

## 참고 항목
- [ATA 필수 구성 요소](/advanced-threat-analytics/PlanDesign/ata-prerequisites)
- [ATA 용량 계획](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)
- [이벤트 수집 구성](/advanced-threat-analytics/PlanDesign/configure-event-collection)
- [Windows 이벤트 전달 구성](/advanced-threat-analytics/PlanDesign/configure-event-collection#ATA_event_WEF)
- [지원이 필요한 경우 포럼을 확인하세요.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


