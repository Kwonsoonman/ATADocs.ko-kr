---
title: "ATA 모니터링 경고 이해 | Microsoft Docs"
description: "ATA 로그를 사용하여 문제를 해결하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b04fb8a4-b366-4b55-9d4c-6f054fa58a90
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0d3b57e852a18bf9602d3a75ab627c23496f7285
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



ATA 상태 관리 센터에서는 모니터링 경고를 생성하여 ATA 배포에 문제가 있을 때 알려줍니다.
이 문서에서는 각 구성 요소에 대한 모든 모니터링 경고를 설명하고 원인 및 문제를 해결하는 데 필요한 단계를 나열합니다.
## <a name="ata-center-issues"></a>ATA 센터 문제
### <a name="center-running-out-of-disk-space"></a>센터에 디스크 공간이 부족함
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 데이터베이스를 저장하는 데 사용되는 ATA 센터 컴퓨터 드라이브의 여유 공간이 부족합니다.|이는 하드 드라이브의 여유 공간이 200GB 미만이거나 20% 여유 공간 중 더 작은 크기임을 의미합니다. ATA가 드라이브의 공간이 부족함을 인식하면 데이터베이스에서 오래된 데이터를 삭제하기 시작합니다. 검색 엔진을 위한 데이터가 필요하기 때문에 오래된 데이터를 삭제할 수 없는 경우 이 경고를 받게 됩니다. 이 경고를 받으면 ATA는 새 활동 추적을 중지합니다.|드라이브 크기를 늘리거나 해당 드라이브에서 공간을 확보합니다.|높은|
### <a name="failure-sending-mail"></a>메일 보내기 실패
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA가 지정된 메일 서버에 메일 알림을 보내지 못했습니다.|ATA에서 메일 메시지가 전송되지 않습니다.|SMTP 서버 구성을 확인합니다.|낮음|

### <a name="center-overloaded"></a>센터가 오버로드됨
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 센터가 ATA 게이트웨이에서 전송되는 데이터 양을 처리할 수 없습니다. |ATA 센터가 새 네트워크 트래픽 및 이벤트 분석을 중지합니다. 이는 이 모니터링 경고가 활성 상태인 동안 검색 및 프로필의 정확도가 감소되었음을 의미합니다.|ATA 센터에 충분한 리소스를 제공했는지 확인합니다. ATA 센터 용량을 제대로 계획하는 방법에 대한 자세한 내용은 [ATA 용량 계획](ata-capacity-planning.md)을 참조하세요. [성능 카운터를 사용하여 ATA 문제 해결](troubleshooting-ata-using-perf-counters.md)에 따라 ATA 센터의 성능을 조사합니다.|높은|

### <a name="failure-connecting-to-the-siem-server-using-syslog"></a>Syslog를 사용하여 SIEM 서버에 연결하지 못함
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA가 지정된 SIEM에 이벤트를 보내지 못했습니다.|이는 ATA 센터가 의심스러운 활동 및 모니터링 경고를 SIEM에 보낼 수 없음을 의미합니다.|[Syslog 서버 설정이 제대로 구성되어 있는지](setting-syslog-email-server-settings.md) 확인합니다.|낮음|
### <a name="center-certificate-is-about-to-expire"></a>센터 인증서가 곧 만료됨
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 센터 인증서가 3주 이내에 만료됩니다.|인증서가 만료되면 ATA 게이트웨이에서 ATA 센터에 연결하지 못합니다. ATA 센터 프로세스가 충돌하고 모든 ATA 기능이 중지됩니다.|[ATA 센터 인증서 바꾸기](modifying-ata-center-configuration.md)|중형|
### <a name="ata-center-certificate-expired"></a>ATA 센터 인증서 만료됨
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 센터 인증서가 만료되었습니다.|인증서가 만료되면 ATA 게이트웨이에서 ATA 센터에 연결하지 못합니다. ATA 센터 프로세스가 충돌하고 모든 ATA 기능이 중지됩니다.|[ATA 센터 인증서 바꾸기](modifying-ata-center-configuration.md)|높은|
## <a name="ata-gateway-issues"></a>ATA 게이트웨이 문제
### <a name="read-only-user-password-to-expire-shortly"></a>읽기 전용 사용자 암호가 곧 만료됨
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|Active Directory에 대해 엔터티 확인을 수행하는 데 사용되는 읽기 전용 사용자 암호가 30일 이내에 만료됩니다.|이 사용자의 암호가 만료되면 모든 ATA 게이트웨이의 실행이 중지되고 새 데이터가 수집되지 않습니다.|[도메인 연결 암호를 변경](modifying-ata-config-dcpassword.md)한 후 ATA 콘솔에서 암호를 업데이트합니다.|중형|
### <a name="read-only-user-password-expired"></a>읽기 전용 사용자 암호 만료됨
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|디렉터리 데이터를 가져오는 데 사용되는 읽기 전용 사용자 암호가 만료되었습니다.|모든 ATA 게이트웨이의 실행이 중지되고(또는 곧 실행 중지됨) 새 데이터가 수집되지 않습니다.|[도메인 연결 암호를 변경](modifying-ata-config-dcpassword.md)한 후 ATA 콘솔에서 암호를 업데이트합니다.|높은|
### <a name="gateway-certificate-about-to-expire"></a>게이트웨이 인증서가 곧 만료됨
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 게이트웨이 인증서가 3주 이내에 만료됩니다.|특정 ATA 게이트웨이에서 ATA 센터에 연결하지 못합니다. 해당 ATA 게이트웨이의 데이터가 전송되지 않습니다.|ATA 게이트웨이 인증서가 자동으로 갱신되었어야 합니다. ATA 게이트웨이 및 ATA 센터 로그를 읽고 인증서가 자동으로 갱신되지 않은 이유를 파악합니다.|중형|

### <a name="gateway-certificate-expired"></a>게이트웨이 인증서가 만료됨
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 게이트웨이 인증서가 만료되었습니다.|이 ATA 게이트웨이에서 ATA 센터로의 연결이 없습니다. 해당 ATA 게이트웨이의 데이터가 전송되지 않습니다.|[ATA 게이트웨이를 제거하고 다시 설치](install-ata-step3.md)합니다.|높은|
### <a name="domain-synchronizer-not-assigned"></a>도메인 동기화 장치가 할당되지 않음
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 게이트웨이에 할당된 도메인 동기화 장치가 없습니다. 이 문제는 도메인 동기화 장치 후보로 구성된 ATA 게이트웨이가 없는 경우에 발생할 수 있습니다.|도메인이 동기화되지 않은 경우 엔터티 변경 내용으로 인해 ATA의 엔터티 정보가 만료 또는 누락될 수도 있지만 검색에는 영향을 주지 않습니다.|하나 이상의 ATA 게이트웨이가 [도메인 동기화 장치](install-ata-step5.md)로 설정되었는지 확인합니다.|낮음|
### <a name="allsome-of-the-capture-network-adapters-on-a-gateway-are-not-available"></a>게이트웨이의 캡처 네트워크 어댑터를 모두/일부 사용할 수 없음
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 게이트웨이에서 선택한 캡처 네트워크 어댑터가 모두/일부 사용할 수 없거나 끊어졌습니다.|ATA 게이트웨이가 일부/모든 도메인 컨트롤러에 대한 네트워크 트래픽을 더 이상 캡처하지 않습니다. 이 경우 해당 도메인 컨트롤러와 관련된 의심스러운 활동을 검색하는 기능에 영향을 줍니다.|ATA 게이트웨이에서 선택한 캡처 네트워크 어댑터가 사용할 수 있고 연결되어 있는지 확인합니다.|중형|
### <a name="some-domain-controllers-are-unreachable-by-a-gateway"></a>게이트웨이가 일부 도메인 컨트롤러에 연결할 수 없음
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|구성된 도메인 컨트롤러 중 일부에 대한 연결 문제 때문에 ATA 게이트웨이의 기능이 제한되었습니다.|ATA 게이트웨이가 일부 도메인 컨트롤러를 쿼리할 수 없는 경우 Pass-the-Hash가 덜 정확할 수 있습니다.|도메인 컨트롤러가 작동하고 실행 중이며 이 ATA 게이트웨이가 도메인 컨트롤러에 대한 LDAP 연결을 열 수 있는지 확인합니다.|중형|
### <a name="all-domain-controllers-are-unreachable-by-a-gateway"></a>게이트웨이가 모든 도메인 컨트롤러에 연결할 수 없음
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|구성된 모든 도메인 컨트롤러에 대한 연결 문제 때문에 ATA 게이트웨이가 현재 오프라인 상태입니다.|이 경우 이 ATA 게이트웨이가 모니터링하는 도메인 컨트롤러와 관련된 의심스러운 활동을 검색하는 ATA 기능에 영향을 줍니다.| 도메인 컨트롤러가 작동하고 실행 중이며 이 ATA 게이트웨이가 도메인 컨트롤러에 대한 LDAP 연결을 열 수 있는지 확인합니다.|중형|
### <a name="gateway-stopped-communicating"></a>게이트웨이 통신 중지
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 게이트웨이에서의 통신이 없었습니다. 이 경고에 대한 기본 시간 범위는 5분입니다.|ATA 게이트웨이의 네트워크 어댑터가 네트워크 트래픽을 더 이상 캡처하지 않습니다. 이 경우 네트워크 트래픽이 ATA 센터에 연결할 수 없으므로 의심스러운 활동을 검색하는 ATA 기능에 영향을 줍니다.|ATA 게이트웨이와 ATA 센터 서비스 간의 통신에 사용되는 포트가 라우터 또는 방화벽에서 차단되지 않는지 확인합니다.|중형|
### <a name="no-traffic-received-from-domain-controller"></a>도메인 컨트롤러에서 받은 트래픽이 없음
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|이 ATA 게이트웨이를 통해 도메인 컨트롤러에서 받은 트래픽이 없었습니다.|이는 도메인 컨트롤러에서 ATA 게이트웨이로의 포트 미러링이 아직 구성되지 않았거나 작동하지 않음을 나타낼 수 있습니다.|[네트워크 장치에 포트 미러링이 제대로 구성되어 있지 않음](configure-port-mirroring.md)을 확인합니다.<br></br>ATA 게이트웨이 캡처 NIC의 고급 설정에서 다음 기능을 사용하지 않도록 설정합니다.<br></br>수신 세그먼트 병합(IPv4)<br></br>수신 세그먼트 병합(IPv6)|중형|
### <a name="some-forwarded-events-are-not-being-analyzed"></a>전달된 일부 이벤트가 분석되고 있지 않음
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 게이트웨이가 처리할 수 있는 것보다 많은 이벤트를 받고 있습니다.|전달된 일부 이벤트가 분석되고 있지 않으므로 이 ATA 게이트웨이가 모니터링 중인 도메인 컨트롤러에서 발생하는 의심스러운 활동을 검색하는 기능에 영향을 줄 수 있습니다.|필요한 이벤트만 ATA 게이트웨이로 전달되었는지 확인하거나, 일부 이벤트를 다른 ATA 게이트웨이로 전달합니다.|중형|
### <a name="some-network-traffic-is-not-being-analyzed"></a>일부 네트워크 트래픽이 분석되고 있지 않음
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 게이트웨이가 처리할 수 있는 것보다 많은 네트워크 트래픽을 받고 있습니다.|전달된 일부 네트워크 트래픽이 분석되고 있지 않으므로 이 ATA 게이트웨이가 모니터링 중인 도메인 컨트롤러에서 발생하는 의심스러운 활동을 검색하는 기능에 영향을 줄 수 있습니다.|필요에 따라 [프로세서 및 메모리 추가](ata-capacity-planning.md)를 고려합니다. 독립 실행형 ATA 게이트웨이인 경우 모니터링 중인 도메인 컨트롤러 수를 줄입니다.<br></br>이는 VMware 가상 컴퓨터에서 도메인 컨트롤러를 사용하는 경우에도 발생할 수 있습니다. 이러한 경고를 방지하기 위해 가상 컴퓨터에서 다음 설정이 0 또는 사용 안 함으로 설정되어 있는지 확인하세요.<br></br>- TsoEnable<br></br>- LargeSendOffload(IPv4)<br></br>- IPv4 TSO Offload<br></br>IPv4 Giant TSO Offload도 사용하지 않도록 설정하는 것이 좋습니다. 자세한 내용은 VMware 설명서를 참조하세요.|중형|

### <a name="gateway-version-outdated"></a>게이트웨이 버전이 만료됨
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 센터가 ATA 게이트웨이에 설치된 버전보다 최신입니다. 이로 인해 ATA 게이트웨이가 예상대로 작동하지 않습니다.|이 경우 이 ATA 게이트웨이가 모니터링 중인 도메인 컨트롤러에서 발생하는 의심스러운 활동을 검색하는 기능에 영향을 줄 수 있습니다.|ATA 콘솔에서 [자동 업데이트](install-ata-step1.md)를 사용하도록 설정하거나 ATA 콘솔에서 사용할 수 있는 최신 ATA 게이트웨이 패키지를 다운로드하여 ATA 게이트웨이를 최신 버전으로 자동으로 업데이트합니다.|높은|
### <a name="gateway-service-failed-to-start"></a>게이트웨이 서비스를 시작하지 못함
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|ATA 게이트웨이 서비스를 30분 이상 시작하지 못했습니다.|이 경우 이 ATA 게이트웨이가 모니터링 중인 도메인 컨트롤러에서 발생하는 의심스러운 활동을 검색하는 기능에 영향을 줄 수 있습니다.|ATA 게이트웨이 로그를 모니터링하여 [ATA 게이트웨이 서비스 오류의 근본 원인을 파악](troubleshooting-ata-using-logs.md)합니다.|높은|
## <a name="lightweight-gateway"></a>경량 게이트웨이
### <a name="lightweight--gateway-reached-a-memory-resource-limit"></a>경량 게이트웨이가 메모리 리소스 제한에 도달함
|경고|설명|해결 방법|심각도|
|----|----|----|----|
|경량 ATA 게이트웨이가 중지되었으며 메모리 부족 상태로부터 도메인 컨트롤러를 보호하기 위해 자동으로 다시 시작됩니다.|경량 ATA 게이트웨이에 자동으로 메모리 제한이 적용되어 도메인 컨트롤러에서 리소스 제한이 발생하지 않도록 합니다. 이 문제는 도메인 컨트롤러의 메모리 사용량이 많은 경우에 발생합니다. 이 도메인 컨트롤러의 데이터가 부분적으로만 모니터링됩니다.|도메인 컨트롤러의 메모리(RAM) 양을 늘리거나, 이 사이트에 도메인 컨트롤러를 추가하여 이 도메인 컨트롤러의 부하를 보다 효율적으로 분산합니다.|중형|


## <a name="see-also"></a>참고 항목
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 용량 계획](ata-capacity-planning.md)
- [이벤트 수집 구성](configure-event-collection.md)
- [Windows 이벤트 전달 구성](configure-event-collection.md#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
