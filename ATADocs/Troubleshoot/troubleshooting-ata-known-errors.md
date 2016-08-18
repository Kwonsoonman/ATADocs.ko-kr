---
title: "ATA 오류 로그 문제 해결 | Microsoft ATA"
description: "ATA의 일반적인 오류를 해결할 수는 방법에 대해 설명합니다."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 6be26fd2d0348557fa7b1c78533eed8a2be1a39f


---

# ATA 오류 로그 문제 해결
이 섹션에서는 ATA 배포 시 발생할 수 있는 오류와 이러한 문제를 해결하는 데 필요한 단계에 대해 자세히 설명합니다.
## ATA 게이트웨이 오류
|오류|설명|해결 방법|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: 로컬 오류가 발생했습니다.|ATA 게이트웨이가 도메인 컨트롤러에 대해 인증하지 못했습니다.|1. DNS 서버에서 도메인 컨트롤러의 DNS 레코드가 올바르게 구성되어 있는지 확인합니다. <br>2. ATA 게이트웨이의 시간이 도메인 컨트롤러의 시간과 동기화되어 있는지 확인합니다.|
|System.IdentityModel.Tokens.SecurityTokenValidationException: 인증서 체인이 유효한지 확인하지 못했습니다.|ATA 게이트웨이가 ATA 센터 인증서의 유효성을 검사하지 못했습니다.|1. 루트 CA 인증서가 ATA 게이트웨이의 신뢰할 수 있는 인증 기관 인증서 저장소에 설치되어 있는지 확인합니다. <br>2. CRL(인증서 해지 목록)을 사용할 수 있는지, 인증서 해지 유효성 검사를 수행할 수 있는지 확인합니다.|
|Microsoft.Common.ExtendedException: 생성된 시간을 구문 분석하지 못했습니다.|ATA 게이트웨이가 SIEM에서 전달된 syslog 메시지를 구문 분석하지 못했습니다.|SIEM이 ATA에서 지원하는 형식 중 하나로 메시지를 전달하도록 구성되어 있는지 확인합니다.|
|System.ServiceModel.FaultException: 메시지에 대한 보안을 확인하는 동안 오류가 발생했습니다.|ATA 게이트웨이가 ATA 센터에 대해 인증하지 못했습니다.|ATA 게이트웨이의 시간이 ATA 센터의 시간과 동기화되어 있는지 확인합니다.|
|System.ServiceModel.EndpointNotFoundException: net.tcp://center.ip.addr:443/IEntityReceiver에 연결할 수 없습니다.|ATA 게이트웨이가 ATA 센터에 연결을 설정하지 못했습니다.|네트워크 설정이 정확한지, ATA 게이트웨이와 ATA 센터 간의 네트워크 연결이 활성 상태인지 확인합니다.|
|System.DirectoryServices.Protocols.LdapException: LDAP 서버를 사용할 수 없습니다.|ATA 게이트웨이가 LDAP 프로토콜을 사용하여 도메인 컨트롤러를 쿼리하지 못했습니다.|1. ATA에서 Active Directory 도메인에 연결하는 데 사용한 사용자 계정이 Active Directory 트리의 모든 개체에 대해 읽기 권한을 갖는지 확인합니다. <br>2. 도메인 컨트롤러가 ATA에서 사용하는 사용자 계정의 LDAP 쿼리를 방지하도록 확정되지 않았는지 확인합니다.|
|Microsoft.Tri.Infrastructure.ContractException: 계약 예외|ATA 게이트웨이가 ATA 센터에서 구성을 동기화하지 못했습니다.|ATA 콘솔에서 ATA 게이트웨이의 구성을 완료합니다.|
|System.Reflection.ReflectionTypeLoadException: 요청된 형식 중 하나 이상을 로드할 수 없습니다. 자세한 내용은 LoaderExceptions 속성을 검색하세요.|Message Analyzer는 ATA 게이트웨이에 설치됩니다.| Message Analyzer를 제거하세요.|
|오류 [레이아웃] System.OutOfMemoryException: 'System.OutOfMemoryException' 유형의 예외가 발생했습니다.|ATA 게이트웨이의 메모리가 부족합니다.|도메인 컨트롤러의 메모리 양을 늘리세요.|
|라이브 소비자 시작 실패  ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: PEFNDIS 이벤트 공급자가 준비되지 않았습니다.|PEF(Message Analyzer)가 올바르게 설치되지 않았습니다.|지원 서비스에 해결 방법을 문의하세요.|
|오류 0x80070652가 발생하여 설치가 실패했습니다.|컴퓨터에서 보류 중인 다른 설치가 있습니다.|다른 설치가 완료될 때까지 기다리고 필요한 경우 컴퓨터를 다시 시작하세요.|

## ATA 콘솔 오류
|오류|설명|해결 방법|
|-------------|----------|---------|
|HTTP 오류 500.19 - 내부 서버 오류|IIS URL 재작성 모듈이 제대로 설치되지 않았습니다.|IIS URL 재작성 모듈을 제거했다가 다시 설치합니다.<br>[IIS URL 재작성 모듈을 다운로드합니다.](http://go.microsoft.com/fwlink/?LinkID=615137)|

## 배포 오류
|오류|설명|해결 방법|
|-------------|----------|---------|
|오류 0x800713ec와 함께 .NET Framework 4.6.1 설치 실패|.Net Framework 4.6.1의 필수 조건이 서버에 설치되어 있지 않습니다. |ATA를 설치하기 전에 Windows 업데이트 [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) 및 [KB2919355](https://support.microsoft.com/kb/2919355)가 서버에 설치되어 있는지 확인합니다.|

![ATA .NET 설치 오류 이미지](media/netinstallerror.png)


## 참고 항목
- [ATA 필수 구성 요소](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 용량 계획](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [이벤트 수집 구성](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Windows 이벤트 전달 구성](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


