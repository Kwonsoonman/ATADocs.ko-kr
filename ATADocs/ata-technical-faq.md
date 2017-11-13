---
title: "Advanced Threat Analytics 질문과 대답 | Microsoft 문서"
description: "ATA에 대한 질문과 관련 대답 목록을 제공합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 25c2defd02e260248d30eb76f6ae297c1b36325f
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*

# <a name="ata-frequently-asked-questions"></a>ATA 질문과 대답
이 문서에서는 ATA에 대한 질문과 관련 정보 및 대답의 목록을 제공합니다.


## <a name="where-can-i-get-a-license-for-advanced-threat-analytics-ata"></a>ATA(Advanced Threat Analytics) 라이선스는 어디서 다운로드할 수 있나요?

활성 기업계약이 있는 경우 VLSC(Microsoft 볼륨 라이선스 센터)에서 소프트웨어를 다운로드할 수 있습니다.

Office 365 포털을 통해 직접 또는 CSP(Cloud Solution Partner) 라이선스 모델을 통해 EMS(Enterprise Mobility + Security)를 구입했으며 VLSC(Microsoft 볼륨 라이선스 센터)를 통해 ATA에 액세스할 수 없는 경우 Microsoft 고객 지원에 ATA(Advanced Threat Analytics)를 활성화하는 프로세스를 문의하세요.

## <a name="what-should-i-do-if-the-ata-gateway-wont-start"></a>ATA 게이트웨이가 시작되지 않으면 어떻게 해야 하나요?
최신 오류 로그에서 가장 최근의 오류를 확인합니다. 오류 로그는 ATA가 설치되어 있는 위치의 “Logs” 폴더에 있습니다.

## <a name="how-can-i-test-ata"></a>ATA를 테스트하려면 어떻게 해야 하나요?
다음 작업 중 하나를 수행하여 종단 간 테스트를 통해 의심스러운 활동을 시뮬레이트할 수 있습니다.

1.  Nslookup.exe를 사용하여 DNS 검색
2.  psexec.exe를 사용하여 원격 실행


이 테스트는 ATA 게이트웨이에서 실행하는 것이 아니라 모니터링 중인 도메인 컨트롤러에 대해 원격으로 실행해야 합니다.

## <a name="which-ata-build-corresponds-to-each-version"></a>각 버전에 해당하는 ATA 빌드는 무엇인가요?

버전 업그레이드 정보는 [ATA 업그레이드 경로](upgrade-path.md)를 참조하세요.

## <a name="what-version-should-i-use-to-upgrade-my-current-ata-deployment-to-the-latest-version"></a>현재 ATA 배포를 최신 버전으로 업그레이드하려면 어떤 버전을 사용해야 하나요?

ATA 버전 업그레이드 행렬은 [ATA 업그레이드 경로](upgrade-path.md)를 참조하세요.


## <a name="how-do-i-verify-windows-event-forwarding"></a>Windows 이벤트 전달을 확인하려면 어떻게 해야 하나요?
파일에 아래의 코드를 넣고 다음과 같이 **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** 디렉터리에서 명령 프롬프트를 통해 명령을 실행할 수 있습니다.

mongo.exe ATA 파일 이름

        db.getCollectionNames().forEach(function(collection) {
        if (collection.substring(0,10)=="NtlmEvent_") {
                if (db[collection].count() > 0) {
                                  print ("Found "+db[collection].count()+" NTLM events") 
                                }
                }
        });

## <a name="does-ata-work-with-encrypted-traffic"></a>암호화된 트래픽에 대해 ATA가 작동하나요?
ATA는 SIEM과 Windows 이벤트 전달에서 수집된 이벤트뿐 아니라 여러 네트워크 프로토콜 분석을 사용하므로 암호화된 트래픽(예: LDAPS 및 IPSEC)이 분석되더라도 대부분의 검색에는 적용되지 않습니다.

## <a name="does-ata-work-with-kerberos-armoring"></a>Kerberos 아머링(armoring)에 대해 ATA가 작동하나요?
FAST(유동 인증 보안 터널링)라고도 하는 Kerberos 아머링(armoring)은 ATA에서 지원됩니다. 단, 해시 검색 통과는 작동하지 않습니다.

## <a name="how-many-ata-gateways-do-i-need"></a>ATA 게이트웨이는 몇 개나 필요한가요?

ATA 게이트웨이 수는 사용 중인 네트워크 레이아웃, 패킷 볼륨과 ATA에서 캡처된 이벤트 볼륨에 따라 다릅니다. 정확한 수를 확인하려면 [ATA 경량 게이트웨이 크기 조정](ata-capacity-planning.md#ata-lightweight-gateway-sizing)을 참조하세요. 

## <a name="how-much-storage-do-i-need-for-ata"></a>ATA용으로 필요한 저장소는 어느 정도인가요?
초당 패킷이 평균 1,000개 생성되는 정규 작업일당 0.3GB의 저장소가 필요합니다.<br /><br />ATA 센터 크기 조정에 대한 자세한 내용은 [ATA 용량 계획](ata-capacity-planning.md)을 참조하세요.


## <a name="why-are-certain-accounts-considered-sensitive"></a>특정 계정을 중요하게 고려하는 이유는 무엇인가요?
중요 그룹으로 지정된 특정 그룹(예: “Domain Admins”)의 구성원인 계정은 중요한 계정으로 간주됩니다.

특정 계정이 중요한 이유를 파악하려면 해당 계정의 그룹 등록을 검토해 계정이 속하는 중요 그룹을 확인할 수 있습니다. 계정이 속해 있는 그룹 역시 다른 중요 그룹에 속해 있어 중요한 그룹으로 간주될 수 있으므로, 최상위 중요 그룹을 찾을 때까지 같은 과정을 수행해야 합니다.

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-ata"></a>ATA를 사용하여 가상 도메인 컨트롤러를 모니터링하려면 어떻게 해야 하나요?
대부분의 가상 도메인 컨트롤러는 ATA 경량 게이트웨이로 다룰 수 있습니다. 사용자 환경에 ATA 경량 게이트웨이가 적절한지 여부를 확인하려면 [ATA 용량 계획](ata-capacity-planning.md)을 참조하세요.

가상 도메인 컨트롤러를 ATA 경량 게이트웨이로 다룰 수 없는 경우에는 [포트 미러링 구성](configure-port-mirroring.md)에 설명된 대로 가상 또는 실제 ATA 게이트웨이를 구성할 수 있습니다.  <br />가장 쉬운 방법은 가상 도메인 컨트롤러가 있는 모든 호스트에 가상 ATA 게이트웨이를 배치하는 것입니다.<br />가상 도메인 컨트롤러가 호스트 간에 이동하는 경우에는 다음 단계 중 하나를 수행해야 합니다.

-   가상 도메인 컨트롤러가 다른 호스트로 이동하는 경우 최근 이동한 가상 도메인 컨트롤러의 트래픽을 받도록 해당 호스트에서 ATA 게이트웨이를 미리 구성합니다.
-   가상 도메인 컨트롤러를 이동하면 가상 ATA 게이트웨이도 함께 이동하도록 가상 도메인 컨트롤러와 가상 ATA 게이트웨이 간에 관계를 설정해야 합니다.
-   호스트 간에 트래픽을 보낼 수 있는 일부 가상 스위치를 사용합니다.

## <a name="how-do-i-back-up-ata"></a>ATA를 백업하려면 어떻게 해야 하나요?

[ATA 재해 복구](disaster-recovery.md)를 참조하세요.



## <a name="what-can-ata-detect"></a>ATA는 어떤 항목을 검색할 수 있나요?

ATA는 알려진 악의적인 공격 및 기법, 보안 문제, 위험을 검색합니다.
전체 ATA 검색 목록은 [ATA에서 수행하는 검색은 무엇인가요?](ata-threats.md)를 참조하세요.

## <a name="what-kind-of-storage-do-i-need-for-ata"></a>ATA에는 어떤 종류의 저장소를 사용해야 하나요?
디스크 액세스 대기 시간이 짧고(10ms 미만) 빠른 저장소(7200RPM 디스크는 권장하지 않음)가 좋습니다. RAID 구성에서 높은 쓰기 부하(RAID-5/6 및 해당 파생 항목은 권장하지 않음)를 지원해야 합니다.

## <a name="how-many-nics-does-the-ata-gateway-require"></a>ATA 게이트웨이에는 NIC가 몇 개나 필요한가요?
ATA 게이트웨이에는 최소 2개의 네트워크 어댑터가 필요합니다.<br>1. 내부 네트워크와 ATA 센터에 연결하기 위한 NIC<br>2. 포트 미러링을 통해 도메인 컨트롤러 네트워크 트래픽을 캡처하는 데 사용될 NIC<br>* 기본적으로 도메인 컨트롤러에서 사용하는 네트워크 어댑터를 모두 사용하는 ATA 경량 게이트웨이에는 적용되지 않습니다.

## <a name="what-kind-of-integration-does-ata-have-with-siems"></a>ATA는 SIEM과 어떤 유형으로 통합할 수 있나요?
다음과 같이 ATA를 SIEM과 양방향으로 통합할 수 있습니다.

1. 의심스러운 활동이 발생하면 CEF 형식을 사용하여 모든 SIEM 서버로 Syslog 경고를 보내도록 ATA를 구성할 수 있습니다.
2. [이러한 SIEM](install-ata-step6.md)에서 Windows 이벤트에 대한 Syslog 메시지를 받도록 ATA를 구성할 수 있습니다.

## <a name="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>ATA는 IaaS 솔루션에 표시되는 도메인 컨트롤러를 모니터링할 수 있나요?
예. ATA 경량 게이트웨이를 사용하여 모든 IaaS 솔루션에 있는 도메인 컨트롤러를 모니터링할 수 있습니다.

## <a name="is-this-an-on-premises-or-in-cloud-offering"></a>ATA는 온-프레미스 제품인가요? 아니면 클라우드 제품인가요?
Microsoft Advanced Threat Analytics는 온-프레미스 제품입니다.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>ATA는 Azure Active Directory 또는 온-프레미스 Active Directory에 포함될 예정인가요?
이 솔루션은 현재 독립 실행형 제품으로 제공되며 Azure Active Directory 또는 온-프레미스 Active Directory에 포함되지 않습니다.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>규칙을 직접 작성하고 임계값/기준을 만들어야 하나요?
Microsoft Advanced Threat Analytics를 사용할 때는 규칙, 임계값 또는 기준을 작성한 다음 미세 조정할 필요가 없습니다. ATA는 사용자, 장치 및 리소스의 동작과 이러한 항목 간의 관계를 분석하며 의심스러운 활동과 알려진 공격을 빠르게 검색할 수 있습니다. 배포 후 3주가 지나면 ATA는 동작이 의심스러운 활동 검색을 시작합니다. 그리고 알려진 악의적 공격 및 보안 문제는 배포 직후부터 검색하기 시작합니다.

## <a name="if-you-are-already-breached-can-microsoft-advanced-threat-analytics-identify-abnormal-behavior"></a>이미 보안이 위반된 경우 Microsoft Advanced Threat Analytics가 비정상 동작을 식별할 수 있나요?
예. ATA는 보안이 위반된 후에 설치하더라도 해커의 의심스러운 활동을 검색할 수 있습니다. ATA는 사용자 동작 자체를 확인할 뿐 아니라, 동작을 조직 보안 맵의 다른 사용자와 대조하여 확인하는 작업도 수행합니다. 초기 분석 시간 중에 확인되는 공격자의 비정상 동작은 "이상값"으로 식별되며 ATA는 비정상 동작을 계속 보고합니다. 또한 ATA는 해커가 Pass-the-Ticket 등의 방식으로 다른 사용자의 자격 증명 도용을 시도하거나 도메인 컨트롤러 중 하나에서 원격 실행을 수행하려는 경우에도 의심스러운 활동을 검색할 수 있습니다.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>ATA는 Active Directory의 트래픽만 활용하나요?
ATA는 심층 패킷 검사 기술을 사용하여 Active Directory 트래픽을 분석할 수 있을 뿐 아니라, SIEM(Security Information and Event Management)에서 관련 이벤트를 수집하고 Active Directory 도메인 서비스의 정보를 기준으로 엔터티 프로필을 만들 수도 있습니다. 또한 조직이 Windows 이벤트 로그 전달을 구성하는 경우 ATA는 이벤트 로그에서 이벤트를 수집할 수도 있습니다.

## <a name="what-is-port-mirroring"></a>포트 미러링이란 무엇인가요?
SPAN(Switched Port Analyzer)이라고도 하는 포트 미러링은 네트워크 트래픽을 모니터링하는 한 방법입니다. 포트 미러링을 사용하도록 설정하면 스위치가 특정 포트 또는 전체 VLAN에서 확인된 모든 네트워크 패킷의 복사본을 다른 포트로 보냅니다. 그러면 이 포트에서 패킷을 분석할 수 있습니다.

## <a name="does-ata-monitor-only-domain-joined-devices"></a>ATA는 도메인에 가입된 장치만 모니터링하나요?
아니요. ATA는 Windows를 사용하지 않는 장치 및 모바일 장치를 포함하여 Active Directory에 대해 인증 및 권한 부여 요청을 수행하는 네트워크의 모든 장치를 모니터링합니다.

## <a name="does-ata-monitor-computer-accounts-as-well-as-user-accounts"></a>ATA는 사용자 계정과 컴퓨터 계정을 모두 모니터링하나요?
예. 컴퓨터 계정 및 기타 모든 엔터티는 악의적인 활동을 수행하는 데 사용될 수 있으므로 ATA는 환경 내의 모든 컴퓨터 계정 동작 및 기타 모든 엔터티를 모니터링합니다.

## <a name="can-ata-support-multi-domain-and-multi-forest"></a>ATA는 다중 도메인 및 다중 포리스트를 지원할 수 있나요?
Microsoft Advanced Threat Analytics는 포리스트 경계가 동일한 다중 도메인 환경을 지원할 예정입니다. 여러 포리스트를 모니터링하려면 별도의 ATA를 배포해야 합니다.

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>배포의 전반적인 상태를 확인할 수 있나요?
예. 배포의 전반적인 상태와 구성/연결 등에 관련된 특정 문제를 모두 확인할 수 있으며, 문제 발생 시 경고가 표시됩니다.


## <a name="see-also"></a>참고 항목
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 용량 계획](ata-capacity-planning.md)
- [이벤트 수집 구성](configure-event-collection.md)
- [Windows 이벤트 전달 구성](configure-event-collection.md#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

