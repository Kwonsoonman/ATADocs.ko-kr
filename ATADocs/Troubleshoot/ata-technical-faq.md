---
# required metadata

title: ATA 기술 FAQ | Microsoft Advanced Threat Analytics
description: ATA에 대한 질문과 관련 대답 목록을 제공합니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 기술 FAQ
이 문서에서는 ATA에 대한 질문과 관련 정보 및 대답의 목록을 제공합니다.

## ATA 질문과 대답

|질문|대답|
|------------|-----------------------------------|
|ATA 게이트웨이가 시작되지 않으면 어떻게 해야 하나요?|최신 오류 로그에서 가장 최근의 오류를 확인합니다. 오류 로그는 ATA가 설치되어 있는 위치의 “Logs” 폴더에 있습니다.|
|ATA를 테스트하려면 어떻게 해야 하나요?|다음 작업 중 하나를 수행하여 종단 간 테스트를 통해 의심스러운 활동을 시뮬레이트할 수 있습니다.<br /><br />1.  Nslookup.exe를 사용하여 DNS 검색<br />2.  psexec.exe를 사용하여 원격 실행<br /><br />이 테스트는 ATA 게이트웨이에서 실행하는 것이 아니라 모니터링 중인 도메인 컨트롤러에 대해 실행해야 합니다.|
|Windows 이벤트 전달을 확인하려면 어떻게 해야 하나요?|**\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** 디렉터리에서 명령 프롬프트를 통해 다음 명령을 실행할 수 있습니다.<br /><br />mongo ATA --eval "printjson(db.getCollectionNames())" &#124; find /C "NtlmEvents"`|
|암호화된 트래픽에 대해 ATA가 작동하나요?|LDAPS, IPSEC ESP 등의 암호화된 트래픽은 분석되지 않습니다.|
|Kerberos 아머링(armoring)에 대해 ATA가 작동하나요?|FAST(유동 인증 보안 터널링)라고도 하는 Kerberos 아머링(armoring)은 ATA에서 지원됩니다. 단, 해시 검색 통과는 작동하지 않습니다.|
|ATA 게이트웨이는 몇 개나 필요한가요?|필요한 게이트웨이 수를 확인할 때는 다음의 두 가지 사항을 고려해야 합니다.<br /><br />-   성능 측면에서 볼 때 도메인 컨트롤러에서 생성되는 총 트래픽의 양에 따라 Active Directory 환경을 처리하는 데 필요한 ATA 게이트웨이의 최소 수가 결정됩니다.<br />    도메인 컨트롤러에서 생성되는 트래픽의 양을 확인하는 방법을 자세히 확인하려면 [ATA 용량 계획](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)을 참조하세요.<br />-   포트 미러링의 작동 제한 역시 모든 도메인 컨트롤러를 지원하는 데 필요한 ATA 게이트웨이의 수(예: 스위치당/데이터 센터당/지역당 게이트웨이 수)를 결정하는 데 영향을 줍니다. 각 환경에서 고유한 사항을 고려해야 합니다.|
|ATA용으로 필요한 저장소는 어느 정도인가요?|초당 패킷이 평균 1,000개 생성되는 정규 작업일당 1.5GB의 저장소가 필요합니다.<br /><br />자세한 내용은 [ATA 용량 계획](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)을 참조하세요.|
|특정 계정이 중요한 이유는 무엇인가요?|중요 그룹으로 지정된 특정 그룹(예: “Domain Admins”)의 구성원인 계정은 중요한 계정으로 간주됩니다.<br />특정 계정이 중요한 이유를 파악하려면 해당 계정의 그룹 등록을 검토해 계정이 속하는 중요 그룹을 확인할 수 있습니다. 계정이 속해 있는 그룹 역시 다른 중요 그룹에 속해 있어 중요한 그룹으로 간주될 수 있으므로, 최상위 중요 그룹을 찾을 때까지 같은 과정을 수행해야 합니다.|
|가상 도메인 컨트롤러를 모니터링하려면 어떻게 해야 하나요?|[포트 미러링 구성](/advanced-threat-analytics/PlanDesign/configure-port-mirroring)의 설명에 따라 가상 또는 실제 ATA 게이트웨이를 배치하면 됩니다.  <br />가장 쉬운 방법은 가상 도메인 컨트롤러가 있는 모든 호스트에 가상 ATA 게이트웨이를 배치하는 것입니다.<br />가상 도메인 컨트롤러가 호스트 간에 이동하는 경우에는 다음 작업 중 하나를 수행해야 합니다.<br /><br />-   가상 도메인 컨트롤러가 다른 호스트로 이동하는 경우 최근 이동한 가상 도메인 컨트롤러의 트래픽을 받도록 해당 호스트에서 ATA 게이트웨이를 미리 구성합니다.<br />-   가상 도메인 컨트롤러를 이동하면 가상 ATA 게이트웨이도 함께 이동하도록 가상 도메인 컨트롤러와 가상 ATA 게이트웨이 간에 관계를 설정해야 합니다.<br />-   호스트 간에 트래픽을 보낼 수 있는 일부 가상 스위치를 사용합니다.|
|ATA를 백업하려면 어떻게 해야 하나요?|다음의 두 가지 항목을 백업합니다.<br /><br />-   데이터베이스에 저장되며 1시간마다 자동으로 백업되는 ATA 구성 <br />-   ATA에서 저장하는 트래픽과 이벤트. 지원되는 모든 데이터베이스 백업 절차를 사용하여 이러한 항목을 백업할 수 있습니다. 자세한 내용은 [ATA 데이터베이스 관리](/advanced-threat-analytics/DeployUse/ata-database-management)를 참조하세요.|
|ATA는 어떤 항목을 검색할 수 있나요?|ATA가 검색하는 모든 항목의 전체 목록은 [Microsoft Advanced Threat Analytics란?](/advanced-threat-analytics/Understand/what-is-ata)을 참조하세요.|
|ATA에는 어떤 종류의 저장소를 사용해야 하나요?|대량의 쓰기 로드를 지원하는 RAID 구성(RAID-5/6 및 여기서 파생된 구성은 제외)이 적용되어 있으며 대기 시간 값이 10ms 미만으로 낮은 고속 저장소(7200RMP 디스크는 제외)를 사용하는 것이 좋습니다.|
|ATA 게이트웨이에는 NIC가 몇 개나 필요한가요?|ATA 게이트웨이에는 최소 2개의 네트워크 어댑터가 필요합니다.<br>1. 내부 네트워크와 ATA 센터에 연결하기 위한 NIC<br>2. 포트 미러링을 통해 도메인 컨트롤러 네트워크를 캡처하기 위한 NIC<br>* 경량 게이트웨이에는 이 요구 사항이 적용되지 않습니다.|
|ATA는 SIEM과 어떤 유형으로 통합할 수 있나요?|다음과 같이 ATA를 SIEM과 양방향으로 통합할 수 있습니다.<br>
1. 의심스러운 활동이 발생하면 CEF 형식을 지원하는 모든 SIEM 서버로 Syslog 경고를 보내도록 ATA를 구성할 수 있습니다.<br>2. [이러한 SIEM](/advanced-threat-analytics/PlanDesign/configure-event-collection#SIEMsupport)에서 ID가 4776인 각 Windows 이벤트에 대해 Syslog 메시지를 받도록 ATA를 구성할 수 있습니다.|


<!--HONumber=Apr16_HO2-->


