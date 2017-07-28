---
title: "데이터베이스를 사용하여 Advanced Threat Analytics 문제 해결 | Microsoft 문서"
description: "ATA 데이터베이스를 사용하여 문제를 해결하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 174918812562b9bfe892fcde90d92e208b26ffc3
ms.sourcegitcommit: 42ce07e3207da10e8dd7585af0e34b51983c4998
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="troubleshooting-ata-using-the-ata-database"></a>ATA 데이터베이스를 사용하여 ATA 문제 해결
ATA는 MongoDB를 데이터베이스로 사용합니다.
기본 명령줄 또는 사용자 인터페이스 도구를 사용하여 데이터베이스와 상호 작용하면서 고급 작업을 수행하고 문제를 해결할 수 있습니다.

## <a name="interacting-with-the-database"></a>데이터베이스와 상호 작용
데이터베이스를 쿼리하는 가장 기본적인 방법은 Mongo 셸을 사용하는 것입니다.

1.  명령줄 창을 열고 MongoDB bin 폴더로 경로를 변경합니다. 기본 경로는 **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**입니다.

2.  `mongo.exe ATA`를 실행합니다. ATA는 모두 대문자로 입력해야 합니다.

> [!div class="mx-tableFixed"]
|사용법|구문|참고|
|-------------|----------|---------|
|데이터베이스에서 컬렉션을 확인합니다.|`show collections`|트래픽이 데이터베이스에 기록 되는지와 이벤트 4776이 ATA에서 수신되는지를 확인하기 위한 종단 간 테스트로 유용합니다.|
|사용자/컴퓨터/그룹(UniqueEntity)의 세부 정보(예: 사용자 ID)를 가져옵니다.|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|특정 날에 특정 컴퓨터에서 시작된 Kerberos 인증 트래픽을 찾습니다.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|&lt;원본 컴퓨터의 ID&gt;를 가져오려면 예제와 같이 UniqueEntity 컬렉션을 쿼리할 수 있습니다.<br /><br />각 네트워크 활동 유형(예: Kerberos 인증)에는 UTC 날짜마다 고유한 컬렉션이 있습니다.|
|특정 날에 특정 계정에 관련된 특정 컴퓨터에서 시작된 NTLM 트래픽을 찾습니다.|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|&lt;원본 컴퓨터의 ID&gt; 및 &lt;계정의 ID&gt;를 가져오려면 예제와 같이 UniqueEntity 컬렉션을 쿼리할 수 있습니다.<br /><br />각 네트워크 활동 유형(예: NTLM 인증)에는 UTC 날짜마다 고유한 컬렉션이 있습니다.|
|계정의 활성화 날짜와 같은 고급 속성을 검색합니다. |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|&lt;계정의 ID&gt;를 가져오려면 예제와 같이 UniqueEntity 컬렉션을 쿼리할 수 있습니다.<br>계정이 활성 상태인 날짜를 표시하는 속성 이름을 "ActiveDates"라고 합니다. 예를 들어 비정상 동작 기계 학습 알고리즘이 실행될 수 있도록 하기 위해 계정에 적어도 21일 동안의 활동이 있는지 확인하려고 할 수 있습니다.|
|고급 구성을 옵션합니다. 이 예제에서 모든 ATA 게이트웨이에 대한 전송 큐 크기를 10,000으로 변경합니다.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

다음 예제에서는 위에 제공된 구문을 사용하는 샘플 코드를 제공합니다. 2015년 10월 20일에 발생한 의심스러운 활동을 조사하고 있으며 "John Doe"가 해당 날짜에 수행한 NTLM 활동에 대해 자세히 알아보려는 경우<br /><br />먼저 "John Doe"의 ID를 찾습니다.

`db.UniqueEntity.find({Name: "John Doe"})`<br>`_id` 값으로 표시된 ID를 적어둡니다. 우리가 사용하는 예제에서는 이 ID를 `123bdd24-b269-h6e1-9c72-7737as875351`(으)로 가정합니다.<br>그런 다음, 찾는 날짜 이전의 가장 가까운 날짜에 해당하는 컬렉션을 검색합니다(현재 예제에서는 2015년 10월 20일).<br>그런 다음 John Doe의 계정 NTLM 활동을 검색합니다. 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

## <a name="see-also"></a>참고 항목
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 용량 계획](ata-capacity-planning.md)
- [이벤트 수집 구성](configure-event-collection.md)
- [Windows 이벤트 전달 구성](configure-event-collection.md#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
