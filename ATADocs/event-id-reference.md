---
title: "ATA 이벤트 ID 참조 | Microsoft Docs"
description: "ATA 이벤트 ID 목록과 해당 설명을 제공합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/25/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 7bd0f90acbb6a2d8eb84fd09bc4d859fff082273
ms.sourcegitcommit: 5563c6861bb5db5cb73e058e5a51b4938b9a7d46
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*


# <a name="ata-event-id-reference"></a>ATA 이벤트 ID 참조

ATA 센터 이벤트 뷰어는 ATA에 대한 이벤트를 기록합니다. 이 문서에서는 이벤트 ID 목록을 제공하고 각각에 대한 설명을 제공합니다.

이벤트는 여기에서 확인할 수 있습니다.

![이벤트 ID 위치](./media/event-id-location.png)

## <a name="ata-health-events"></a>ATA 상태 이벤트

1001 - ATA 센터 데이터베이스 데이터 드라이브 여유 공간 상태 경고 

1003 – ATA 센터 오버로드된 상태 경고 

1004 – 인증서 만료 상태 경고 

1005 – 센터 데이터베이스 연결이 끊김 상태 경고 

1006 – ATA Gateway 디렉터리 서비스 클라이언트 계정 암호 만료 상태 경고 

1007 – ATA Gateway 도메인 동기화 장치 할당되지 않음 상태 경고 

1008 – ATA Gateway 캡처 네트워크 어댑터 오류 발생 상태 경고 

1009 – ATA Gateway 캡처 네트워크 어댑터 누락 상태 경고 

1010 – ATA Gateway 디렉터리 서비스 클라이언트 연결 상태 경고 

1011 – ATA Gateway 연결이 끊김 상태 경고 

1012 - ATA Gateway 오버로드 이벤트 작업 상태 경고 

1013 - ATA Gateway 오버로드 네트워크 작업 상태 경고 

1014 - 센터 메일 상태 경고 

1015 - 센터 Syslog 상태 경고 

1016 – ATA Gateways 만료 상태 경고 

1017 – 트래픽을 수신하지 못한 센터 상태 경고 

1018 – ATA Gateway 시작 실패 상태 경고 

1019 – ATA Gateway 메모리 부족 상태 경고 

1020 – ATA Gateway RADIUS 이벤트 수신기 상태 경고 

1021 – ATA Gateway Syslog 이벤트 수신기 상태 경고 

1022 – ATA 센터 외부 IP 주소 확인 실패 상태 경고 
 
## <a name="ata-suspicious-ctivity-events"></a>ATA 의심스러운 작업 이벤트

2001 - 비정상 동작 의심스러운 작업 

2002 - 비정상 프로토콜 의심스러운 작업 

2003 – 계정 열거형 의심스러운 작업 

2004 - LDAP 무차별 암호 대입(Brute force) 의심스러운 작업 

2005 - 컴퓨터 사전 인증 실패 의심스러운 작업 

2006 - 디렉터리 서비스 복제 의심스러운 작업 

2007 - DNS 정찰 의심스러운 작업 

2008 - 암호화 다운그레이드 의심스러운 작업 

2012 - 열거형 세션 의심스러운 작업 

2013 - 위조된 PAC 의심스러운 작업 

2014 - Honeytoken 작업 의심스러운 작업 

2015 - LDAP 일반 텍스트 암호 의심스러운 작업 

2016 - 대규모 개체 삭제 의심스러운 작업 

2017 - 해시 의심스러운 작업 전달 

2018 - 티켓 의심스러운 작업 전달 

2019 – 원격 실행 의심스러운 작업 

2020 – 데이터 보호 백업 키 의심스러운 작업 검색 

2021 - SAMR 정찰 의심스러운 작업 

2022 - 골든 티켓 의심스러운 작업 

2023 – 비정상 중요 그룹 멤버 자격 변경 의심스러운 작업 

2023 - 무차별 암호 대입(Brute force) 의심스러운 작업 

## <a name="ata-auditing-events"></a>ATA 감사 이벤트

3001 – ATA 구성으로 변경 

3002 – ATA Gateway 추가

3003 – ATA Gateway 삭제

3004 - ATA 라이선스 활성화

3005 – ATA 콘솔에 로그인

3006 – 상태 작업 상태로 수동 변경 

3007 – 의심스러운 작업 상태로 수동 변경 


## <a name="see-also"></a>참고 항목
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 용량 계획](ata-capacity-planning.md)
- [이벤트 수집 구성](configure-event-collection.md)
- [Windows 이벤트 전달 구성](configure-event-collection.md#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
