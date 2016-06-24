---
# required metadata

title: 성능 카운터를 사용하여 ATA 문제 해결 | Microsoft Advanced Threat Analytics
description: 성능 카운터를 사용하여 ATA 문제를 해결하는 방법을 설명합니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: df162a62-f273-4465-9887-94271f5000d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 성능 카운터를 사용하여 ATA 문제 해결
ATA 성능 카운터는 ATA의 각 구성 요소에 대한 성능 정보를 제공합니다.

**ATA 구성 요소 프로세스**:

1.  구성 요소가 최대 크기에 도달하면 이전 구성 요소에서 추가 엔터티를 보내는 것을 차단합니다.

2.  그러면 이전 구성 요소가 그 이전 구성 요소의 추가 엔터티 보내기를 차단할 때까지 **자체** 크기를 늘리기 시작합니다.

3.  이는 더 이상 엔터티를 전달할 수 없을 때 트래픽을 삭제하는 초기 NetworkListener 구성 요소까지 거슬러 올라갑니다.

    즉, 트래픽 삭제를 일으키는 체인 반응을 해결하려면 체인 끝단의 문제를 해결해야 합니다.
    내부 ATA 구성 요소의 흐름을 이해하려면 [ATA 아키텍처](/advanced-threat-analytics/Understand/ata-architecture)를 참조하세요.

## ATA Gateway 성능 카운터
ATA Gateway의 성능 카운터를 추가하여 ATA Gateway의 실시간 성능 상태를 관찰할 수 있습니다.
이 작업을 수행하려면 "성능 모니터"를 열고 ATA Gateway에 대한 모든 카운터를 추가합니다. 성능 카운터 개체의 이름은 "Microsoft ATA Gateway"입니다.

![성능 카운터 추가 이미지](media/ATA-performance-counters.png)

다음은 주의해야 하는 주 ATA Gateway 카운터 목록입니다.

|카운터|설명|Threshold|문제 해결|
|-----------|---------------|-------------|-------------------|
|NetworkListener Captured Parser Messages/Sec|ATA Gateway가 1초마다 처리하는 트래픽 양입니다.|임계값 없음|ATA Gateway에서 구문 분석되는 트래픽 양을 이해하도록 도와줍니다.|
|NetworkListener Captured Dropped Messages/Sec|ATA Gateway가 1초마다 삭제하는 트래픽 양입니다.|이 숫자는 항상 0이어야 합니다(드물게 발생하는 삭제의 짧은.버스트는 허용됨).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|NetworkListener Captured Dropped ETW Real Time Buffers/Sec|ATA Gateway가 1초마다 삭제하는 트래픽 양입니다.|이 숫자는 항상 0이어야 합니다(드물게 발생하는 삭제의 짧은.버스트는 허용됨).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|NetworkListener Captured Dropped ETW Log Buffers/Sec|ATA Gateway가 1초마다 삭제하는 트래픽 양입니다.|이 숫자는 항상 0이어야 합니다(드물게 발생하는 삭제의 짧은.버스트는 허용됨).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|NetworkListener Captured Dropped ETW Events/Sec|ATA Gateway가 1초마다 삭제하는 트래픽 양입니다.|이 숫자는 항상 0이어야 합니다(드물게 발생하는 삭제의 짧은.버스트는 허용됨).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|NetworkActivityTranslator Message Data # Block Size|NA(네트워크 활동)로 변환되기 위해 큐에서 대기 중인 트래픽 양입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 100,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|EntityResolver Activity Block Size|해결을 위해 큐에서 대기 중인 NA(네트워크 활동) 양입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 10,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|EntitySender Entity Batch Block Size|ATA Center로 전송되기 위해 큐에서 대기 중인 NA(네트워크 활동) 양입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 1,000,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|EntitySender Batch Send Time|마지막 일괄 처리를 전송하는 데 걸린 시간의 양입니다.|대부분 1000밀리초 미만이어야 합니다.|ATA Gateway와 ATA Center 간에 네트워킹 문제가 있는지 확인합니다.|

> [!NOTE]
> -   시간 카운터는 밀리초 단위입니다.
> -   경우에 따라 "보고서" 그래프 종류를 사용하여 전체 카운터 목록을 모니터링하는 것이 보다 편리한 경우가 있습니다(예: 모든 카운터의 실시간 모니터링).

## ATA Center 성능 카운터
ATA Center의 성능 카운터를 추가하여 ATA Center의 실시간 성능 상태를 관찰할 수 있습니다.

이 작업을 수행하려면 "성능 모니터"를 열고 ATA Center에 대한 모든 카운터를 추가합니다. 성능 카운터 개체의 이름은 "Microsoft ATA Center"입니다.

![ATA Center 성능 카운터 추가](media/ATA-Gateway-perf-counters.png)

다음은 주의해야 하는 주 ATA Center 카운터 목록입니다.

|카운터|설명|Threshold|문제 해결|
|-----------|---------------|-------------|-------------------|
|EntityReceiver Entity Batch Block Size|ATA Center에서 큐에 넣은 엔터티 일괄 처리 수입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 100).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다.  위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|NetworkActivityProcessor Network Activity Block Size|처리를 위해 큐에서 대기 중인 NA(네트워크 활동) 수입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 10,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|EntityProfiler Network Activity Block Size|프로파일링을 위해 큐에서 대기 중인 NA(네트워크 활동) 수입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 10,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|CenterDatabaseClient &#42; Block Size|데이터베이스에 기록되기 위해 큐에서 대기 중인 특정 유형의 네트워크 활동 수입니다.|최대값 - 1보다 작아야 합니다(기본 최대값: 50,000).|최대 크기에 도달하고 NetworkListener까지의 이전 구성 요소를 차단하는 구성 요소가 있는지 확인합니다. 위의 **ATA 구성 요소 프로세스**를 참조하세요.<br /><br />CPU 또는 메모리에 문제가 없는지 확인합니다.|
|DetectionEngine Detection Time|결정적 검색의 마지막 전체 주기에 소요된 총 시간입니다.|900,000(15분) 미만이어야 합니다.|CPU, 메모리 또는 저장소에 문제가 없는지 확인합니다.|

> [!NOTE]
> -   시간 카운터는 밀리초 단위입니다.
> -   경우에 따라 보고서에 대한 그래프 종류를 사용하여 전체 카운터 목록을 모니터링하는 것이 보다 편리한 경우가 있습니다(예: 모든 카운터의 실시간 모니터링).

다음은 주의해야 하는 주 운영 체제 카운터 목록입니다.

|카운터|설명|Threshold|문제 해결|
|-----------|---------------|-------------|-------------------|
|Processor(_Total)\% Processor Time|프로세서가 비유휴 스레드를 실행하는 데 걸린 경과된 시간의 백분율입니다.|평균 80% 미만|프로세서 시간이 예상보다 훨씬 많이 걸리는 특정 프로세스가 있는지 확인합니다.<br /><br />프로세서를 더 추가합니다.<br /><br />서버당 트래픽 양을 줄입니다.<br /><br />"Processor(_Total)\% Processor Time" 카운터는 가상 서버에서 정확도가 떨어질 수 있습니다. 부족한 프로세서 능력을 보다 정확하게 측정하는 방법은 "System\Processor Queue Length" 카운터를 사용하는 것입니다.|
|System\Context Switches/sec|모든 프로세서가 스레드 간에 전환된 결합된 비율입니다.|코어(물리적 코어) 5000개&#42; 미만|프로세서 시간이 예상보다 훨씬 많이 걸리는 특정 프로세스가 있는지 확인합니다.<br /><br />프로세서를 더 추가합니다.<br /><br />서버당 트래픽 양을 줄입니다.<br /><br />"Processor(_Total)\% Processor Time" 카운터는 가상 서버에서 정확도가 떨어질 수 있습니다. 부족한 프로세서 능력을 보다 정확하게 측정하는 방법은 "System\Processor Queue Length" 카운터를 사용하는 것입니다.|
|System\Processor Queue Length|실행 준비가 완료되고 예약 대기 중인 스레드 수입니다.|코어(물리적 코어) 5개&#42; 미만|프로세서 시간이 예상보다 훨씬 많이 걸리는 특정 프로세스가 있는지 확인합니다.<br /><br />프로세서를 더 추가합니다.<br /><br />서버당 트래픽 양을 줄입니다.<br /><br />"Processor(_Total)\% Processor Time" 카운터는 가상 서버에서 정확도가 떨어질 수 있습니다. 부족한 프로세서 능력을 보다 정확하게 측정하는 방법은 "System\Processor Queue Length" 카운터를 사용하는 것입니다.|
|Memory\Available MBytes|할당할 수 있는 실제 메모리(RAM) 양입니다.|512보다 커야 합니다.|실제 메모리를 예상보다 훨씬 많이 사용하는 특정 프로세스가 있는지 확인합니다.<br /><br />실제 메모리 양을 늘립니다.<br /><br />서버당 트래픽 양을 줄입니다.|
|LogicalDisk(&#42;)\Avg. Disk sec/Read 성능 카운터를 수집합니다.|디스크에서 데이터를 읽는 평균 대기 시간입니다(데이터베이스 드라이브를 인스턴스로 선택해야 함).|10밀리초 미만이어야 합니다.|데이터베이스 드라이브를 예상보다 많이 활용하는 특정 프로세스가 있는지 확인합니다.<br /><br />저장소 팀/공급업체에 이 드라이브가 10밀리초 미만의 대기 시간 동안 현재 워크로드를 전달할 수 있는지 문의합니다. 현재 워크로드는 디스크 사용률 카운터를 사용하여 확인할 수 있습니다.|
|LogicalDisk(&#42;)\Avg. Disk sec/Write|디스크에 데이터를 쓰는 평균 대기 시간입니다(데이터베이스 드라이브를 인스턴스로 선택해야 함).|10밀리초 미만이어야 합니다.|데이터베이스 드라이브를 예상보다 많이 활용하는 특정 프로세스가 있는지 확인합니다.<br /><br />저장소 팀/공급업체에 이 드라이브가 10밀리초 미만의 대기 시간 동안 현재 워크로드를 전달할 수 있는지 문의합니다. 현재 워크로드는 디스크 사용률 카운터를 사용하여 확인할 수 있습니다.|
|\LogicalDisk(&#42;)\Disk Reads/sec|디스크에 대한 읽기 작업을 수행하는 비율입니다.|임계값 없음|디스크 사용률 카운터는 저장소 대기 시간 문제를 해결할 때 정보를 추가할 수 있습니다.|
|\LogicalDisk(&#42;)\Disk Read Bytes/sec|초당 디스크에서 읽은 바이트 수입니다.|임계값 없음|디스크 사용률 카운터는 저장소 대기 시간 문제를 해결할 때 정보를 추가할 수 있습니다.|
|\LogicalDisk(&#42;)\Disk Writes/sec|디스크에 대한 쓰기 작업을 수행하는 비율입니다.|임계값 없음|디스크 사용률 카운터(저장소 대기 시간 문제를 해결할 때 정보를 추가할 수 있음)|
|\LogicalDisk(&#42;)\Disk Write Bytes/sec|초당 디스크에 쓴 바이트 수입니다.|임계값 없음|디스크 사용률 카운터는 저장소 대기 시간 문제를 해결할 때 정보를 추가할 수 있습니다.|


<!--HONumber=Apr16_HO2-->


