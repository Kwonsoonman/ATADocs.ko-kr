---
title: "성능 카운터를 사용하여 Advanced Threat Analytics 문제 해결 | Microsoft 문서"
description: "성능 카운터를 사용하여 ATA 문제를 해결하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: df162a62-f273-4465-9887-94271f5000d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ae72f7a25f0c57dadd02049fe3a570a0da7b84fd
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/30/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# 성능 카운터를 사용하여 ATA 문제 해결
<a id="troubleshooting-ata-using-the-performance-counters" class="xliff"></a>
ATA 성능 카운터는 ATA의 각 구성 요소에 대한 성능 정보를 제공합니다. ATA의 구성 요소는 데이터를 순차적으로 처리하므로 문제가 발생할 경우 구성 요소 체인에 따라 어딘가에 부분적으로 삭제된 트래픽을 유발할 수 있습니다. 이 문제를 해결하려면 역효과를 낳는 구성 요소를 파악하고 연쇄 반응의 시작이 되는 문제를 해결해야 합니다. 성능 카운터에서 찾은 데이터를 사용하여 각 구성 요소의 작동 방식을 이해합니다.
내부 ATA 구성 요소의 흐름을 이해하려면 [ATA 아키텍처](ata-architecture.md)를 참조하세요.

**ATA 구성 요소 프로세스**:

1.  구성 요소가 최대 크기에 도달하면 이전 구성 요소에서 추가 엔터티를 보내는 것을 차단합니다.

2.  그러면 이전 구성 요소가 그 이전 구성 요소의 추가 엔터티 보내기를 차단할 때까지 **자체** 크기를 늘리기 시작합니다.

3.  이는 더 이상 엔터티를 전달할 수 없을 때 트래픽을 삭제하는 NetworkListener 구성 요소까지 거슬러 올라갑니다.


## 문제 해결에 대한 성능 모니터 파일 검색하기
<a id="retrieving-performance-monitor-files-for-troubleshooting" class="xliff"></a>

ATA 구성 요소에서 성능 모니터 파일(BLG)를 검색하려면:
1.  성능 모니터를 엽니다.
2.  “Microsoft ATA Gateway” 또는 “Microsoft ATA Center”라는 이름으로 지정된 데이터 수집기 집합을 중지합니다.
3.  데이터 수집기 집합 폴더로 이동합니다(기본적으로 이 폴더는 "C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs\DataCollectorSets" 또는 “C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs\DataCollectorSets”입니다).
4.  가장 최근에 수정된 BLG 파일을 복사합니다.
5.  “Microsoft ATA Gateway” 또는 “Microsoft ATA Center”라는 이름으로 지정된 데이터 수집기 집합을 다시 시작합니다.


## ATA Gateway 성능 카운터
<a id="ata-gateway-performance-counters" class="xliff"></a>

이 섹션에서는 ATA 게이트웨이에 대한 모든 참조가 ATA 경량 게이트웨이와도 관련됩니다.

ATA Gateway의 성능 카운터를 추가하여 ATA Gateway의 실시간 성능 상태를 관찰할 수 있습니다.
이 작업을 수행하려면 "성능 모니터"를 열고 ATA Gateway에 대한 모든 카운터를 추가합니다. 성능 카운터 개체의 이름은 "Microsoft ATA Gateway"입니다.

다음은 주의해야 하는 주 ATA Gateway 카운터 목록입니다.

|카운터|설명|Threshold|문제 해결|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway\NetworkListener PEF Parsed Messages\Sec|ATA Gateway가 1초마다 처리하는 트래픽 양입니다.|임계값 없음|ATA Gateway에서 구문 분석되는 트래픽 양을 이해하도록 도와줍니다.|
|NetworkListener PEF Dropped Events\Sec|ATA Gateway가 1초마다 삭제하는 트래픽 양입니다.|이 숫자는 항상 0이어야 합니다(드물게 발생하는 삭제의 짧은.버스트는 허용됨).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|Microsoft ATA Gateway\NetworkListener ETW Dropped Events\Sec|ATA Gateway가 1초마다 삭제하는 트래픽 양입니다.|이 숫자는 항상 0이어야 합니다(드물게 발생하는 삭제의 짧은.버스트는 허용됨).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|Microsoft ATA Gateway\NetworkActivityTranslator Message Data # Block Size|NA(네트워크 활동)로 변환되기 위해 큐에서 대기 중인 트래픽 양입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 100,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|Microsoft ATA Gateway\EntityResolver Activity Block Size|해결을 위해 큐에서 대기 중인 NA(네트워크 활동) 양입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 10,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|Microsoft ATA Gateway\EntitySender Entity Batch Block Size|ATA Center로 전송되기 위해 큐에서 대기 중인 NA(네트워크 활동) 양입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 1,000,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|Microsoft ATA Gateway\EntitySender Batch Send Time|마지막 일괄 처리를 전송하는 데 걸린 시간의 양입니다.|대부분 1000밀리초 미만이어야 합니다.|ATA Gateway와 ATA Center 간에 네트워킹 문제가 있는지 확인합니다.|

> [!NOTE]
> -   시간 카운터는 밀리초 단위입니다.
> -   경우에 따라 "보고서" 그래프 종류를 사용하여 전체 카운터 목록을 모니터링하는 것이 보다 편리한 경우가 있습니다(예: 모든 카운터의 실시간 모니터링).

## ATA 경량 게이트웨이 성능 카운터
<a id="ata-lightweight-gateway-performance-counters" class="xliff"></a>
성능 카운터는 ATA가 설치된 도메인 컨트롤러에서 너무 많은 리소스를 사용되지 않도록 경량 게이트웨이에서 할당량 관리에 사용할 수 있습니다.
경량 게이트웨이에서 ATA가 적용하는 리소스 제한을 확인하려면 이 카운터를 추가합니다.

이 작업을 수행하려면 "성능 모니터"를 열고 ATA 경량 게이트웨이에 대한 모든 카운터를 추가합니다. 성능 카운터 개체 이름은 "Microsoft ATA Gateway" 및 "Microsoft ATA Gateway Updater"입니다.


|카운터|설명|Threshold|문제 해결|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager CPU Time Max %|경량 게이트웨이 프로세스에서 사용할 수 있는 최대 CPU 시간(%)입니다. |임계값 없음 | 이 카운터는 도메인 컨트롤러 리소스가 ATA 경량 게이트웨이에서 사용되지 않도록 제한합니다. 시간이 지날수록 프로세스가 자주 최대 한도에 도달하면(프로세스가 한도에 도달하면 트래픽 삭제가 시작됨) 도메인 컨트롤러를 실행하는 서버에 좀 더 많은 리소스를 추가해야 한다는 것을 의미합니다.|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Commit Memory Max Size|경량 게이트웨이 프로세스에서 사용할 수 있는 최대 커밋된 메모리 크기(바이트)입니다.|임계값 없음 | 이 카운터는 도메인 컨트롤러 리소스가 ATA 경량 게이트웨이에서 사용되지 않도록 제한합니다. 시간이 지날수록 프로세스가 자주 최대 한도에 도달하면(프로세스가 한도에 도달하면 트래픽 삭제가 시작됨) 도메인 컨트롤러를 실행하는 서버에 좀 더 많은 리소스를 추가해야 한다는 것을 의미합니다.| 
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager Working Set Limit Size|경량 게이트웨이 프로세스에서 사용할 수 있는 최대 실제 메모리 크기(바이트)입니다.|임계값 없음 | 이 카운터는 도메인 컨트롤러 리소스가 ATA 경량 게이트웨이에서 사용되지 않도록 제한합니다. 시간이 지날수록 프로세스가 자주 최대 한도에 도달하면(프로세스가 한도에 도달하면 트래픽 삭제가 시작됨) 도메인 컨트롤러를 실행하는 서버에 좀 더 많은 리소스를 추가해야 한다는 것을 의미합니다.|



실제 사용 내용을 보려면 다음 카운터를 참조하세요.



|카운터|설명|Threshold|문제 해결|
|-----------|---------------|-------------|-------------------|
|Process(Microsoft.Tri.Gateway)\%Processor Time|경량 게이트웨이 프로세스에서 실제로 사용하는 CPU 시간(%)입니다. |임계값 없음 | 이 카운터 결과를 GatewayUpdaterResourceManager CPU Time Max %의 한도와 비교합니다. 시간이 지날수록 프로세스가 자주 최대 한도에 도달하면(프로세스가 한도에 도달하면 트래픽 삭제가 시작됨) 좀 더 많은 리소스를 경량 게이트웨이 전용으로 사용해야 한다는 것을 의미합니다.|
|Process(Microsoft.Tri.Gateway)\Private Bytes|경량 게이트웨이 프로세스에서 실제로 사용하는 커밋된 메모리 크기(바이트)입니다.|임계값 없음 | 이 카운터 결과를 GatewayUpdaterResourceManager Commit Memory Max Size의 한도와 비교합니다. 시간이 지날수록 프로세스가 자주 최대 한도에 도달하면(프로세스가 한도에 도달하면 트래픽 삭제가 시작됨) 좀 더 많은 리소스를 경량 게이트웨이 전용으로 사용해야 한다는 것을 의미합니다.| 
|Process(Microsoft.Tri.Gateway)\Working Set|경량 게이트웨이 프로세스에서 실제로 사용하는 실제 메모리 크기(바이트)입니다.|임계값 없음 |이 카운터 결과를 GatewayUpdaterResourceManager Working Set Limit Size의 한도와 비교합니다. 시간이 지날수록 프로세스가 자주 최대 한도에 도달하면(프로세스가 한도에 도달하면 트래픽 삭제가 시작됨) 좀 더 많은 리소스를 경량 게이트웨이 전용으로 사용해야 한다는 것을 의미합니다.|

## ATA Center 성능 카운터
<a id="ata-center-performance-counters" class="xliff"></a>
ATA 센터의 성능 카운터를 추가하여 ATA 센터의 실시간 성능 상태를 관찰할 수 있습니다.

이 작업을 수행하려면 "성능 모니터"를 열고 ATA Center에 대한 모든 카운터를 추가합니다. 성능 카운터 개체의 이름은 "Microsoft ATA Center"입니다.

다음은 주의해야 하는 주 ATA Center 카운터 목록입니다.

|카운터|설명|Threshold|문제 해결|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Center\EntityReceiver Entity Batch Block Size|ATA Center에서 큐에 넣은 엔터티 일괄 처리 수입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 10,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다.  위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|Microsoft ATA Center\NetworkActivityProcessor Network Activity Block Size|처리를 위해 큐에서 대기 중인 NA(네트워크 활동) 수입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 50,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|Microsoft ATA Center\EntityProfiler Network Activity Block Size|프로파일링을 위해 큐에서 대기 중인 NA(네트워크 활동) 수입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 10,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|Microsoft ATA Center\Database &#42; Block Size|데이터베이스에 기록되기 위해 큐에서 대기 중인 특정 유형의 네트워크 활동 수입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 50,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|


> [!NOTE]
> -   시간 카운터는 밀리초 단위입니다.
> -   경우에 따라 보고서에 대한 그래프 종류를 사용하여 전체 카운터 목록을 모니터링하는 것이 보다 편리한 경우가 있습니다(예: 모든 카운터의 실시간 모니터링).

## 운영 체제 카운터
<a id="operating-system-counters" class="xliff"></a>
다음은 주의해야 하는 주 운영 체제 카운터 목록입니다.

|카운터|설명|Threshold|문제 해결|
|-----------|---------------|-------------|-------------------|
|Processor(_Total)\% Processor Time|프로세서가 비유휴 스레드를 실행하는 데 걸린 경과된 시간의 백분율입니다.|평균 80% 미만|프로세서 시간이 예상보다 훨씬 많이 걸리는 특정 프로세스가 있는지 확인합니다.<br /><br />프로세서를 더 추가합니다.<br /><br />서버당 트래픽 양을 줄입니다.<br /><br />"Processor(_Total)\% Processor Time" 카운터는 가상 서버에서 정확도가 떨어질 수 있습니다. 부족한 프로세서 능력을 보다 정확하게 측정하는 방법은 "System\Processor Queue Length" 카운터를 사용하는 것입니다.|
|System\Context Switches\sec|모든 프로세서가 스레드 간에 전환된 결합된 비율입니다.|코어(물리적 코어) 5000개&#42; 미만|프로세서 시간이 예상보다 훨씬 많이 걸리는 특정 프로세스가 있는지 확인합니다.<br /><br />프로세서를 더 추가합니다.<br /><br />서버당 트래픽 양을 줄입니다.<br /><br />"Processor(_Total)\% Processor Time" 카운터는 가상 서버에서 정확도가 떨어질 수 있습니다. 부족한 프로세서 능력을 보다 정확하게 측정하는 방법은 "System\Processor Queue Length" 카운터를 사용하는 것입니다.|
|System\Processor Queue Length|실행 준비가 완료되고 예약 대기 중인 스레드 수입니다.|코어(물리적 코어) 5개&#42; 미만|프로세서 시간이 예상보다 훨씬 많이 걸리는 특정 프로세스가 있는지 확인합니다.<br /><br />프로세서를 더 추가합니다.<br /><br />서버당 트래픽 양을 줄입니다.<br /><br />"Processor(_Total)\% Processor Time" 카운터는 가상 서버에서 정확도가 떨어질 수 있습니다. 부족한 프로세서 능력을 보다 정확하게 측정하는 방법은 "System\Processor Queue Length" 카운터를 사용하는 것입니다.|
|Memory\Available MBytes|할당할 수 있는 실제 메모리(RAM) 양입니다.|512보다 커야 합니다.|실제 메모리를 예상보다 훨씬 많이 사용하는 특정 프로세스가 있는지 확인합니다.<br /><br />실제 메모리 양을 늘립니다.<br /><br />서버당 트래픽 양을 줄입니다.|
|LogicalDisk(&#42;)\Avg. Disk sec\Read|디스크에서 데이터를 읽는 평균 대기 시간입니다(데이터베이스 드라이브를 인스턴스로 선택해야 함).|10밀리초 미만이어야 합니다.|데이터베이스 드라이브를 예상보다 많이 활용하는 특정 프로세스가 있는지 확인합니다.<br /><br />저장소 팀/공급업체에 이 드라이브가 10밀리초 미만의 대기 시간 동안 현재 워크로드를 전달할 수 있는지 문의합니다. 현재 워크로드는 디스크 사용률 카운터를 사용하여 확인할 수 있습니다.|
|LogicalDisk(&#42;)\Avg. Disk sec\Write|디스크에 데이터를 쓰는 평균 대기 시간입니다(데이터베이스 드라이브를 인스턴스로 선택해야 함).|10밀리초 미만이어야 합니다.|데이터베이스 드라이브를 예상보다 많이 활용하는 특정 프로세스가 있는지 확인합니다.<br /><br />저장소 팀/공급업체에 이 드라이브가 10밀리초 미만의 대기 시간 동안 현재 워크로드를 전달할 수 있는지 문의합니다. 현재 워크로드는 디스크 사용률 카운터를 사용하여 확인할 수 있습니다.|
|\LogicalDisk(&#42;)\Disk Reads\sec|디스크에 대한 읽기 작업을 수행하는 비율입니다.|임계값 없음|디스크 사용률 카운터는 저장소 대기 시간 문제를 해결할 때 정보를 추가할 수 있습니다.|
|\LogicalDisk(&#42;)\Disk Read Bytes\sec|초당 디스크에서 읽은 바이트 수입니다.|임계값 없음|디스크 사용률 카운터는 저장소 대기 시간 문제를 해결할 때 정보를 추가할 수 있습니다.|
|\LogicalDisk&#42;\Disk Writes\sec|디스크에 대한 쓰기 작업을 수행하는 비율입니다.|임계값 없음|디스크 사용률 카운터(저장소 대기 시간 문제를 해결할 때 정보를 추가할 수 있음)|
|\LogicalDisk(&#42;)\Disk Write Bytes\sec|초당 디스크에 쓴 바이트 수입니다.|임계값 없음|디스크 사용률 카운터는 저장소 대기 시간 문제를 해결할 때 정보를 추가할 수 있습니다.|

## 참고 항목
<a id="see-also" class="xliff"></a>
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 용량 계획](ata-capacity-planning.md)
- [이벤트 수집 구성](configure-event-collection.md)
- [Windows 이벤트 전달 구성](configure-event-collection.md#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
