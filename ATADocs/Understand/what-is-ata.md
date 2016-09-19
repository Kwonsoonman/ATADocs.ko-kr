---
title: "Microsoft ATA(Advanced Threat Analytics)란? | Microsoft ATA"
description: "Microsoft ATA(Advanced Threat Analytics)의 정의와 검색할 수 있는 의심스러운 활동의 종류를 설명합니다."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: c2f8d642f5ab0927448730453873a5b6271b3d2b


---

*적용 대상: Advanced Threat Analytics 버전 1.7*


## Advanced Threat Analytics란?
ATA(Advanced Threat Analytics)는 여러 유형으로 대상이 지정된 고급 사이버 공격과 내부자 위협으로부터 기업을 보호하는 온-프레미스 플랫폼입니다.

## ATA의 작동 방법
ATA는 네트워크의 로그와 이벤트에서 여러 데이터 소스의 정보를 사용하여 사용자 동작과 조직의 다른 엔티티를 학습하고 이에 대한 동작 프로필을 만듭니다.
ATA는 다음으로부터 이벤트와 로그를 받을 수 있습니다.

-   SIEM 통합
-   WEF(Windows 이벤트 전달)

또한 ATA는 독점 네트워크 구문 분석 엔진을 활용하여 인증 및 정보 수집을 위해 여러 프로토콜(예: Kerberos, DNS, RPC, NTLM 및 기타)의 네트워크 트래픽을 캡처하고 구문 분석합니다. 이 정보는 다음을 통해 ATA에서 수집됩니다.

-   도메인 컨트롤러와 DNS 서버에서 ATA 게이트웨이로의 포트 미러링
-   도메인 컨트롤러에 ATA LGW(경량 게이트웨이) 직접 배포

ATA 아키텍처에 대한 자세한 내용은 [ATA 아키텍처](/advanced-threat-analytics/plan-design/ata-architecture)를 참조하세요.

ATA의 소개 비디오를 확인해 보세요!
<iframe width="560" height="315" src="https://www.youtube.com/embed/0nA9FeTRZFw" frameborder="0" allowfullscreen></iframe>

## ATA의 기능

ATA 기술에서는 다음과 같이 사이버 공격를 적극 대처하는 여러 단계에 중점을 두고 여러 의심스러운 활동을 검색합니다.

-   정찰. 공격자가 환경이 구축된 방법, 다음 공격 단계를 위해 일반적으로 계획을 수립하는 다른 자산과 엔터티에 대한 정보를 수집하는 동안 수행합니다.
-   측면 활동 주기. 공격자가 네트워크 내부에서 공격 진영을 분산하기 위해 시간과 노력을 들이는 동안 수행합니다.
-   도메인 선점(지속성). 공격자가 다양한 진입점, 자격 증명 및 기술을 사용하여 공격 작전을 다시 시작할 수 있도록 정보를 캡처하는 동안 수행합니다. 

이러한 사이버 공격 단계는 공격을 받는 회사나 대상이 되는 정보 유형에 상관없이 유사하며, 예측 가능합니다.
ATA는 세 가지 종류의 공격, 악의적인 공격, 비정상적인 동작, 그리고 보안 문제 및 위험을 검색합니다.

**악의적인 공격**은 다음을 비롯한 알려진 공격 유형의 전체 목록을 검색하여 확정적으로 검색됩니다.

-   PtT(Pass-the-Ticket)
-   PtH(Pass-the-Hash)
-   Overpass-the-Hash
-   위조된 PAC(MS14-068)
-   골든 티켓
-   악의적인 복제
-   정찰
-   무차별 암호 대입(Brute force)
-   원격 실행

검색과 검색에 대한 설명이 포함된 전체 목록은 [ATA에서 검색할 수 있는 의심스러운 활동은 무엇인가요?](ata-threats.md)를 참조하세요.
ATA는 이러한 의심스러운 활동을 검색하고 누가, 무엇을, 언제, 어떻게 활동했는지 명확하게 설졍하는 보기를 포함하여 ATA 콘솔에 정보를 제공합니다. 이렇게 간단하고 알기 쉬운 대시보드를 모니터링함으로써 네트워크의 클라이언트 1과 클라이언트 2 컴퓨터에서 Pass-the-Hash 공격이 시도되었음을 ATA에서 검색하여 경고 메시지를 받게 됩니다.

 ![샘플 ATA Pass-the-Hash](media/sample screen pth.png)

**비정상적인 사용자 동작**은 ATA에서 동작 분석을 사용하고 Machine Learning 기능을 활용하여 다음을 비롯한 네트워크에서 사용자와 장치의 의심스러운 활동과 비정상 동작을 파악함으로써 검색됩니다.

-   비정상적인 로그인
-   알 수 없는 위협
-   암호 공유
-   측면 확대


이러한 종류의 의심스러운 활동은 ATA 대시보드에서 볼 수 있습니다. 다음 예에서 ATA는 사용자가 일반적으로 액세스 하지 않는 4대의 컴퓨터에 액세스한 경우(알림의 원인이 될 수 있음) 경고를 보냅니다.

 ![샘플 ATA 화면 비정상적인 동작](media/sample screen abnormal behavior.png) 

ATA는 또한 다음을 포함하여 **보안 문제 및 위험**을 검색합니다.

-   손상된 신뢰
-   약한 프로토콜
-   알려진 프로토콜 취약점

이러한 종류의 의심스러운 활동은 ATA 대시보드에서 볼 수 있습니다. 다음 예에서 ATA는 네트워크의 컴퓨터와 도메인 간의 손상된 신뢰 관계가 있음을 알립니다.

  ![샘플 ATA 화면 손상된 신뢰](media/sample screen broken trust.png)


## 다음 단계

-   ATA가 네트워크에 적용되는 방식에 대한 자세한 내용은 [ATA 아키텍처](/advanced-threat-analytics/plan-design/ata-architecture)를 참조하세요.

-   ATA 배포를 시작하려면 [ATA 설치](/advanced-threat-analytics/deploy-use/install-ata)를 참조하세요.

## 참고 항목
[ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


