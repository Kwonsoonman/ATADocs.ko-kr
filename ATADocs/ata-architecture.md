---
title: "Advanced Threat Analytics 아키텍처 | Microsoft 문서"
description: "Microsoft Advanced Threat Analytics(ATA)의 아키텍처에 대해 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 66f5678285c203476aee3daafae22ac7b34d0ae2
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*




# <a name="ata-architecture"></a>ATA 아키텍처
아래 다이어그램에는 Advanced Threat Analytics 아키텍처가 자세히 나와 있습니다.

![ATA 아키텍처 토폴로지 다이어그램](media/ATA-architecture-topology.jpg)

ATA는 실제 또는 가상 스위치를 사용하는 ATA 게이트웨이에 포트 미러링을 활용하여 도메인 컨트롤러 네트워크 트래픽을 모니터링합니다. 도메인 컨트롤러에 직접 ATA 경량 게이트웨이를 배포하는 경우 포트 미러링에 대한 요구 사항이 제거됩니다. 또한 ATA는 Windows 이벤트(SIEM 서버 또는 도메인 컨트롤러에서 직접 전달됨)를 활용하고 공격 및 위협에 대한 데이터를 분석할 수 있습니다.
이 섹션에서는 네트워크 및 이벤트 캡처의 흐름을 설명하고, ATA의 주요 구성 요소(ATA 게이트웨이, ATA 경량 게이트웨이(ATA 게이트웨이와 같은 핵심 기능이 있음), ATA 센터)의 기능을 설명하기 위해 드릴다운합니다.


![ATA 트래픽 흐름 다이어그램](media/ATA-traffic-flow.jpg)

## <a name="ata-components"></a>ATA 구성 요소
ATA는 다음 구성 요소로 이루어져 있습니다.

-   **ATA 센터** <br>
ATA 센터는 사용자가 배포하는 ATA 게이트웨이 및/또는 ATA 경량 게이트웨이에서 데이터를 수신합니다.
-   **ATA 게이트웨이**<br>
ATA 게이트웨이는 포트 미러링 또는 네트워크 TAP를 사용하여 도메인 컨트롤러의 트래픽을 모니터링하는 전용 서버에 설치됩니다.
-   **ATA 경량 게이트웨이**<br>
ATA 경량 게이트웨이는 도메인 컨트롤러에 직접 설치되며 전용 서버 또는 포트 미러링 구성 없이 트래픽을 직접 모니터링합니다. ATA 게이트웨이를 대신합니다.

ATA 배포는 모든 ATA 게이트웨이, 모든 ATA 경량 게이트웨이 또는 ATA 게이트웨이와 ATA 경량 게이트웨이의 조합과 연결된 단일 ATA 센터로 구성될 수 있습니다.


## <a name="deployment-options"></a>배포 옵션
ATA는 다음과 같은 게이트웨이 조합을 사용하여 배포할 수 있습니다.

-   **ATA 게이트웨이만 사용** <br>
ATA 배포에 ATA 경량 게이트웨이 없이 ATA 게이트웨이만 포함될 수 있습니다. 이 경우 ATA 게이트웨이에 대해 포트 미러링을 사용하도록 모든 도메인 컨트롤러를 구성하거나, 네트워크 TAP가 준비되어 있어야 합니다.
-   **ATA 경량 게이트웨이만 사용**<br>
ATA 배포에 ATA 경량 게이트웨이만 포함될 수 있습니다. 이 경우 ATA 경량 게이트웨이가 각 도메인 컨트롤러에 배포되며, 서버 또는 포트 미러링을 추가로 구성하지 않아도 됩니다.
-   **ATA 게이트웨이와 ATA 경량 게이트웨이 사용**<br>
ATA 배포에는 ATA 게이트웨이와 ATA 경량 게이트웨이가 둘 다 포함됩니다. ATA 경량 게이트웨이는 일부 도메인 컨트롤러(예: 분기 사이트의 모든 도메인 컨트롤러)에 설치됩니다. 이와 동시에 다른 도메인 컨트롤러는 ATA 게이트웨이(예: 주 데이터 센터의 더 큰 도메인 컨트롤러)에 의해 모니터링됩니다.

이러한 모든 시나리오에서 모든 게이트웨이는 해당 데이터를 ATA 센터로 보냅니다.




## <a name="ata-center"></a>ATA Center
**ATA 센터**는 다음 기능을 수행합니다.

-   ATA 게이트웨이 및 ATA 경량 게이트웨이 구성 설정 관리

-   ATA 게이트웨이 및 ATA 경량 게이트웨이에서 데이터 수신 

-   의심스러운 활동 검색

-   ATA 동작 기계 학습 알고리즘을 실행하여 비정상적인 동작 검색

-   다양한 결정적 알고리즘을 실행하여 공격 중단 체인에 따라 고급 공격 검색

-   ATA 콘솔 실행

-   선택 사항: 의심스러운 활동이 검색되면 전자 메일과 이벤트를 보내도록 ATA 센터 구성 가능

ATA 센터는 ATA 게이트웨이 및 ATA 경량 게이트웨이에서 구문 분석된 트래픽을 받습니다. 그런 다음 프로파일링을 수행하고 기계 학습 및 동작 알고리즘을 실행하여 네트워크 관련 정보를 학습하고 비정상을 검색하며 의심스러운 활동을 경고합니다.

|||
|-|-|
|엔터티 수신기|모든 ATA 게이트웨이 및 ATA 경량 게이트웨이에서 엔터티 배치를 받습니다.|
|네트워크 활동 처리기|받은 각 배치 내의 모든 네트워크 활동을 처리합니다. 예를 들어 서로 다를 수 있는 컴퓨터에서 수행한 여러 Kerberos 단계가 일치하는지를 확인합니다.|
|엔터티 프로파일러|트래픽과 이벤트에 따라 모든 고유 엔터티를 프로파일링합니다. 예를 들어 ATA는 각 사용자 프로필에 대해 로그온한 컴퓨터 목록을 업데이트합니다.|
|Center 데이터베이스|네트워크 활동과 이벤트를 데이터베이스에 기록하는 프로세스를 관리합니다. |
|데이터베이스|ATA는 MongoDB를 사용하여 다음과 같은 시스템의 모든 데이터를 저장합니다.<br /><br />-   네트워크 활동<br />-   이벤트 활동<br />-   고유 엔터티<br />-   의심스러운 활동<br />-   ATA 구성|
|탐지기|탐지기는 기계 학습 알고리즘과 결정적 규칙을 사용하여 네트워크에서 의심스러운 활동과 비정상적인 사용자 동작을 찾습니다.|
|ATA 콘솔|ATA 콘솔은 ATA를 구성하고 네트워크에서 ATA가 검색한 의심스러운 활동을 모니터링하는 데 사용됩니다. ATA 콘솔은 ATA 센터 서비스 실행 여부와 관계없이 실행됩니다. 즉, 서비스가 중지되어도 ATA 콘솔은 데이터베이스와 통신할 수 있으면 실행됩니다.|
네트워크에서 배포할 ATA 센터의 수를 결정할 때는 다음 조건을 고려하세요.

-   각 ATA 센터는 Active Directory 포리스트 하나를 모니터링할 수 있습니다. Active Directory 포리스트가 둘 이상인 경우에는 Active Directory 포리스트당 최소 하나의 ATA 센터가 필요합니다.

-    대규모 Active Directory 배포에서는 ATA 센터 하나가 모든 도메인 컨트롤러의 트래픽을 모두 처리하지 못할 수도 있습니다. 이 경우 ATA 센터가 여러 개 있어야 합니다. ATA 센터의 수는 [ATA 용량 계획](ata-capacity-planning.md)에 따라 결정해야 합니다.

## <a name="ata-gateway-and-ata-lightweight-gateway"></a>ATA 게이트웨이 및 ATA 경량 게이트웨이

### <a name="gateway-core-functionality"></a>게이트웨이 핵심 기능
**ATA 게이트웨이** 및 **ATA 경량 게이트웨이** 둘 다 다음과 같은 동일한 핵심 기능이 있습니다.

-   도메인 컨트롤러 네트워크 트래픽 캡처 및 검사. ATA 게이트웨이의 경우 포트 미러링된 트래픽이고, ATA 경량 게이트웨이에서는 도메인 컨트롤러의 로컬 트래픽입니다. 

-   Windows 이벤트 전달 기능을 통해 SIEM 또는 Syslog 서버나 도메인 컨트롤러에서 Windows 이벤트 수신

-   Active Directory 도메인에서 사용자 및 컴퓨터에 대한 데이터 검색

-   네트워크 엔터티(사용자, 그룹, 컴퓨터) 확인 수행

-   ATA 센터에 관련 데이터 전송

-   단일 ATA 게이트웨이의 여러 도메인 컨트롤러를 모니터링하거나 ATA 경량 게이트웨이의 단일 도메인 컨트롤러를 모니터링합니다.

ATA 게이트웨이는 네트워크에서 네트워크 트래픽과 Windows 이벤트를 수신하여 다음과 같은 기본 구성 요소에서 처리합니다.

|||
|-|-|
|네트워크 수신기|네트워크 수신기는 네트워크 트래픽을 캡처하고 트래픽을 구문 분석합니다. 이러한 작업에서는 CPU를 많이 사용하므로 ATA 게이트웨이 또는 ATA 경량 게이트웨이를 계획할 때는 [ATA 필수 구성 요소](ata-prerequisites.md)를 확인하는 것이 특히 중요합니다.|
|이벤트 수신기|이벤트 수신기는 네트워크의 SIEM 서버에서 전달되는 Windows 이벤트를 캡처하고 구문 분석합니다.|
|Windows 이벤트 로그 판독기|Windows 이벤트 로그 판독기는 도메인 컨트롤러에서 ATA 게이트웨이의 Windows 이벤트 로그로 전달된 Windows 이벤트를 읽고 구문 분석합니다.|
|네트워크 활동 변환기 | 구문 분석된 트래픽을 ATA에서 사용되는 논리적 트래픽 표현(NetworkActivity)으로 변환합니다.
|엔터티 확인자|엔터티 확인자는 구문 분석된 데이터(네트워크 트래픽 및 이벤트)를 가져와 Active Directory에서 확인하여 계정 및 ID 정보를 찾습니다. 그러면 해당 정보가 구문 분석된 데이터에 있는 IP 주소와 연결됩니다. 패킷 헤더를 효율적으로 검사하고, 인증 패킷에서 컴퓨터 이름/속성/ID를 구문 분석할 수 있도록 설정합니다. 구문 분석된 인증 패킷을 실제 패킷의 데이터와 결합합니다.|
|엔터티 발신자|엔터티 발신자는 구문 분석되어 일치 여부가 확인된 데이터를 ATA 센터로 보냅니다.|

## <a name="ata-lightweight-gateway-features"></a>ATA 경량 게이트웨이 기능

다음 기능은 ATA 게이트웨이 또는 ATA 경량 게이트웨이 실행 여부에 따라 다르게 작동합니다.

-   ATA 경량 게이트웨이가 이벤트 전달을 구성하지 않고도 로컬에서 이벤트를 읽을 수 있습니다.

-   **도메인 동기화 장치 후보**<br>
도메인 동기화 게이트웨이는 특정 Active Directory 도메인의 모든 엔터티를 적극적으로 동기화합니다(도메인 컨트롤러 자체에서 복제에 사용하는 메커니즘과 유사). 후보 목록에서 하나의 게이트웨이가 임의로 선택되어 도메인 동기화 장치 역할을 합니다. <br><br>
동기화 장치가 30분 이상 오프라인 상태인 경우 다른 후보가 대신 선택됩니다. 특정 도메인에 사용할 수 있는 도메인 동기화 장치가 없는 경우 ATA는 엔터티 및 해당 변경 사항을 사전에 동기화할 수 있지만, 모니터링되는 트래픽에서 감지되는 경우 새 엔터티를 사후에 검색합니다. 
<br>사용 가능한 도메인 동기화 장치가 없고 관련된 트래픽이 없는 엔터티를 검색하는 경우 검색 결과가 표시되지 않습니다.<br><br>
기본적으로 모든 ATA 게이트웨이는 동기화 장치 후보입니다.<br><br>
모든 ATA 경량 게이트웨이는 분기 사이트 및 작은 도메인 컨트롤러에 배포될 가능성이 더 높기 때문에 기본적으로 동기화 장치 후보가 아닙니다.


-   **리소스 제한 사항**<br>
ATA 경량 게이트웨이에는 이 게이트웨이가 실행되고 있는 도메인 컨트롤러에서 사용 가능한 계산 및 메모리 용량을 평가하는 모니터링 구성 요소가 포함됩니다. 모니터링 프로세스는 10초 마다 실행되며, 도메인 컨트롤러에 특정 시점에 사용 가능한 계산 및 메모리 리소스의 15% 이상이 있도록 ATA 경량 게이트웨이 프로세스에 대한 CPU 및 메모리 사용률 할당량을 동적으로 업데이트합니다.<br><br>
도메인 컨트롤러에 수행되는 작업에 관계없이 이 프로세스는 항상 도메인 컨트롤러의 핵심 기능에 영향을 주지 않도록 리소스를 확보합니다.<br><br>
이로 인해 ATA 경량 게이트웨이에 리소스 부족이 발생하면 일부 트래픽만 모니터링되고, 상태 페이지에 “Dropped port mirrored network traffic”(포트 미러링된 네트워크 트래픽이 삭제됨)이라는 모니터링 경고가 표시됩니다.

다음 표에서는 현재 필요한 용량보다 더 많은 할당량을 사용하여 모든 트래픽을 모니터링할 수 있을 만큼 계산 리소스가 충분한 도메인 컨트롤러의 예를 제공합니다.

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory(Lsass.exe)|ATA 경량 게이트웨이(Microsoft.Tri.Gateway.exe)|기타(기타 프로세스) |ATA 경량 게이트웨이 할당량|게이트웨이 삭제|
|30%|20%|10%|45%|아니요|

Active Directory에 더 많은 계산이 필요한 경우 ATA 경량 게이트웨이에서 필요한 할당량이 줄어듭니다. 다음 예제에서는 ATA 경량 게이트웨이에 할당된 할당량 보다 더 많은 양이 필요하여 일부 트래픽을 삭제합니다(일부 트래픽만 모니터링).

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory(Lsass.exe)|ATA 경량 게이트웨이(Microsoft.Tri.Gateway.exe)|기타(기타 프로세스) |ATA 경량 게이트웨이 할당량|게이트웨이 삭제 비율|
|60%|15%|10%|15%|예|


## <a name="your-network-components"></a>네트워크 구성 요소
ATA에서 작업하려면 다음 구성 요소가 설정되어 있는지 확인하세요.

### <a name="port-mirroring"></a>포트 미러링
ATA 게이트웨이를 사용하는 경우 실제 또는 가상 스위치를 사용하여 ATA 게이트웨이를 대상으로 모니터링하고 설정할 도메인 컨트롤러에 대해 포트 미러링을 설정해야 합니다. 또 다른 옵션은 네트워크 TAP를 사용하는 것입니다. 도메인 컨트롤러 전체가 아닌 일부를 모니터링하는 경우 ATA가 작동되지만 검색 효율성은 떨어집니다.

포트 미러링이 ATA 게이트웨이에 대한 모든 도메인 컨트롤러 네트워크 트래픽을 미러링하지만 해당 트래픽 중 일부분만이 분석을 위해 압축되어 ATA 센터로 전송됩니다.

도메인 컨트롤러와 ATA 게이트웨이는 실제 하드웨어일 수도 있고 가상 하드웨어일 수도 있습니다. 자세한 내용은 [포트 미러링 구성](configure-port-mirroring.md)을 참조하세요.


### <a name="events"></a>이벤트
Pass-the-Hash, 무차별 암호 대입(Brute force), 중요한 그룹 수정, Honeytoken에 대한 ATA 검색을 개선하려면 ATA에 Windows 이벤트 4776, 4732, 4733, 4728, 4729, 4756, 4757이 필요합니다. 이러한 이벤트는 ATA 경량 게이트웨이에서 자동으로 읽거나, ATA 경량 게이트웨이가 배포되지 않은 경우 두 가지 방법 중 하나로 ATA 게이트웨이에 전달될 수 있습니다. 하나는 ATA 게이트웨이가 SIEM 이벤트를 수신하도록 구성하는 것이고, 다른 하나는 [Windows 이벤트 전달을 구성](#configuring-windows-event-forwarding)하는 것입니다.

-   SIEM 이벤트를 수신하도록 ATA 게이트웨이 구성 <br>특정 Windows 이벤트를 ATA로 전달하도록 SIEM을 구성합니다. ATA는 다수의 SIEM 공급업체를 지원합니다. 자세한 내용은 [이벤트 수집 구성](configure-event-collection.md)을 참조하세요.

-   Windows 이벤트 전달 구성<br>ATA가 이벤트를 받을 수 있도록 하는 또 다른 방법은, Windows 이벤트 4776, 4732, 4733, 4728, 4729, 4756 및 4757을 ATA 게이트웨이로 전달하도록 도메인 컨트롤러를 구성하는 것입니다. SIEM이 없거나 SIEM이 현재 ATA에서 지원되지 않는 경우 이 방법을 사용하면 특히 유용합니다. ATA의 Windows 이벤트 전달 기능에 대한 자세한 내용은 [Windows 이벤트 전달 구성](configure-event-collection.md#configuring-windows-event-forwarding)을 참조하세요. 이는 실제 ATA 게이트웨이에만 적용되고 ATA 경량 게이트웨이에는 적용되지 않습니다.

## <a name="related-videos"></a>관련 동영상
- [올바른 ATA 게이트웨이 유형 선택](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>참고 항목
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 크기 조정 도구](http://aka.ms/atasizingtool)
- [ATA 용량 계획](ata-capacity-planning.md)
- [이벤트 수집 구성](configure-event-collection.md)
- [Windows 이벤트 전달 구성](configure-event-collection.md#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

