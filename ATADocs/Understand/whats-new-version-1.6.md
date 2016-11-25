---
title: "ATA 버전 1.6의 새로운 기능 | Microsoft ATA"
description: "알려진 문제와 함께 ATA 버전 1.6의 새로운 기능을 나열합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 27b139e5-12b9-4953-8f53-eb58e8ce0038
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: fca7f1b2b8260cad6e0ce32aad1c9e1b53fc0ad5
ms.openlocfilehash: 2cf155b0a54d12e78b5cac5be1ac077786e8cd07


---

# <a name="whats-new-in-ata-version-16"></a>ATA 버전 1.6의 새로운 기능
이 릴리스 정보에서는 이 버전의 Advanced Threat Analytics에서 알려진 문제에 대한 정보를 제공합니다.

## <a name="whats-new-in-the-ata-16-update"></a>ATA 1.6 업데이트의 새로운 기능
ATA 1.6 업데이트에서는 다음 영역에 대한 향상된 기능을 제공합니다.

-   새 검색

-   기존 검색 기능 개선

-   ATA 경량 게이트웨이

-   자동 업데이트

-   향상된 ATA 센터 성능

-   저장소 요구 사항 감소

-   IBM QRadar 지원

### <a name="new-detections"></a>새 검색


- **악성 데이터 보호 개인 정보 요청** DPAPI(데이터 보호 API)는 암호 기반 데이터 보호 서비스입니다. 이 보호 서비스는 웹 사이트 암호 및 파일 공유 자격 증명과 같은 사용자의 비밀 정보를 저장하는 다양한 응용 프로그램에서 사용됩니다. 암호 손실 시나리오를 지원하기 위해 사용자는 자신의 암호를 포함하지 않는 복구 키를 사용하여 보호된 데이터를 해독할 수 있습니다. 도메인 환경에서 공격자가 복구 키를 원격으로 도용하고 사용하여 도메인에 가입된 모든 컴퓨터에서 보호된 데이터를 해독할 수 있습니다.


- **넷 세션 열거** 정찰은 고급 공격 중단 체인의 주요 단계입니다. DC(도메인 컨트롤러)는 SMB(서버 메시지 블록) 프로토콜을 사용하여 그룹 정책 개체를 배포하기 위한 파일 서버 역할을 합니다. 정찰 단계의 일부로 공격자가 DC에서 서버에 있는 모든 활성 SMB 세션을 쿼리하여 해당 SMB 세션과 연결된 모든 사용자 및 IP 주소에 액세스하도록 할 수 있습니다. SMB 세션 열거는 공격자가 중요한 계정을 대상으로 지정하는 데 사용되어 네트워크를 가로로 이동하는 데 도움을 줄 수 있습니다.


- **악의적인 복제 요청** Active Directory 환경에서는 도메인 컨트롤러 간에 복제가 자주 수행됩니다. 공격자가 Active Directory 복제 요청을 스푸핑(경우에 따라 도메인 컨트롤러를 가장)하여 볼륨 섀도 복사본과 같이 방해하는 기술을 사용하지 않고도 암호 해시를 비롯하여 Active Directory에 저장된 데이터를 검색할 수 있습니다.


- **MS11-013 취약점 탐지** Kerberos에는 특정 측면의 Kerberos 서비스 티켓이 위조될 수 있는 권한 상승 취약성이 있습니다. 악의적인 사용자나 이 취약점을 악용하는 공격자가 도메인 컨트롤러에서 상승된 권한으로 토큰을 얻을 수 있습니다.


- **비정상적인 프로토콜 구현** 인증 요청(Kerberos 또는 NTLM)은 일반적으로 표준 메서드 및 프로토콜 집합을 사용하여 수행됩니다. 그러나 성공적으로 인증하려면 요청이 특정 요구 사항 집합을 충족해야만 합니다. 공격자가 환경에서 표준 구현과 약간의 차이로 이러한 프로토콜을 구현할 수 있습니다. 이러한 차이를 통해 Pass-The-Hash, 무차별 암호 대입(Brute Force) 등의 공격을 실행하려는 공격자가 있음을 알 수 있습니다.


### <a name="improvements-to-existing-detections"></a>기존 검색 기능 개선
ATA 1.6은 골든 티켓, 허니토큰, 무차별 암호 대입(Brute Force), 원격 실행 등 기존 검색에 대해 거짓 긍정 및 거짓 부정 시나리오를 줄이는 향상된 검색 논리를 제공합니다.

### <a name="the-ata-lightweight-gateway"></a>ATA 경량 게이트웨이
이 버전의 ATA에서는 ATA 게이트웨이에 새로운 배포 옵션을 제공하여 ATA 게이트웨이를 도메인 컨트롤러에 직접 설치할 수 있습니다. 이 배포 옵션에서는 ATA 게이트웨이의 중요하지 않은 기능을 제거하고 DC에서 사용 가능한 리소스를 기반으로 하는 동적 리소스 관리를 제공하여 DC의 기존 작업이 영향을 받지 않도록 합니다. ATA 경량 게이트웨이를 사용하면 ATA 배포 비용을 줄일 수 있습니다. 동시에 하드웨어 리소스 용량이 제한되거나 포트 미러링 지원을 설정할 수 없는 분기 사이트에서의 배포가 더 쉬워집니다.
ATA 경량 게이트웨이에 대한 자세한 내용은 [ATA 아키텍처](/advanced-threat-analytics/plan-design/ata-architecture#ata-gateway-and-ata-lightweight-gateway)를 참조하세요.

배포 고려 사항 및 적합한 게이트웨이 유형 선택에 대한 자세한 내용은 [ATA 용량 계획](/advanced-threat-analytics/plan-design/ata-capacity-planning#choosing-the-right-gateway-type-for-your-deployment)을 참조하세요.


### <a name="automatic-updates"></a>자동 업데이트
버전 1.6부터는 Microsoft Update를 사용하여 ATA 센터를 업데이트할 수 있습니다. 또한 ATA 게이트웨이는 ATA 센터와의 표준 통신 채널을 사용하여 자동으로 업데이트할 수 있습니다.
### <a name="improved-ata-center-performance"></a>향상된 ATA 센터 성능
이 버전에서는 데이터베이스 부하가 줄고 모든 검색을 보다 효율적인 방법으로 실행하여 단일 ATA 센터로 훨씬 더 많은 도메인 컨트롤러를 모니터링할 수 있습니다.

### <a name="lower-storage-requirements"></a>저장소 요구 사항 감소
ATA 1.6에서 ATA 데이터베이스를 실행하는 데 필요한 저장소 공간이 현저하게 줄어 이전 버전에서 사용된 저장소 공간의 20%만 있으면 됩니다.

### <a name="support-for-ibm-qradar"></a>IBM QRadar 지원
이제 ATA는 이전에 지원된 SIEM 솔루션뿐만 아니라 IBM의 QRadar SIEM 솔루션에서도 이벤트를 받을 수 있습니다.

## <a name="known-issues"></a>알려진 문제
이 버전에는 다음과 같은 알려진 문제가 존재합니다.

### <a name="failure-to-recognize-new-path-in-manually-moved-databases"></a>수동으로 이동된 데이터베이스에서 새 경로를 인식하지 못함

데이터베이스 경로가 수동으로 이동된 배포에서 ATA 배포는 업데이트에 새 데이터베이스 경로 사용하지 않습니다. 따라서 다음과 같은 문제가 발생할 수 있습니다.


- ATA가 기존 네트워크 활동을 순환적으로 삭제하지 않고 ATA 센터의 시스템 드라이브에서 사용 가능한 공간을 모두 사용할 수 있습니다.


- ATA를 버전 1.6으로 업데이트하면 다음 이미지와 같이 업데이트 전 준비 검사에 실패할 수 있습니다.
    ![준비 검사 실패](media/ata_failed_readinesschecks.png)
    >[!Important]
ATA를 버전 1.6으로 업데이트하기 전에 올바른 데이터베이스 경로를 사용하여 다음 레지스트리 키를 업데이트하세요. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath`

### <a name="migration-failure-when-updating-from-ata-15"></a>ATA 1.5에서 업데이트할 때 마이그레이션 실패
ATA 1.6으로 업데이트할 때 다음 오류 코드로 인해 업데이트 프로세스가 실패할 수 있습니다.

![ATA 1.6 업데이트 오류](http://i.imgur.com/QrLSApr.png) 이 오류가 표시되는 경우 **C:\Users\<User>\AppData\Local\Temp**, and look for the following exception에서 배포 로그를 검토하고 다음 예외를 찾습니다.

    System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> MongoDB.Driver.MongoWriteException: A write operation resulted in an error. E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : "<guid>" } ---> MongoDB.Driver.MongoBulkWriteException`1: A bulk write operation resulted in one or more errors.  E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : " <guid> " }

'System.ArgumentNullException: 값은 null일 수 없습니다.'라는 오류 메시지가 표시될 수도 있습니다.
    
이러한 오류 중 하나가 있는 경우 다음 해결 방법을 실행하세요.

**해결 방법**: 

1.  "data_old" 폴더를 임시 폴더(일반적으로 %ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin에 있음)로 이동합니다.
2.  ATA 센터 v1.5를 제거하고 모든 데이터베이스 데이터를 삭제합니다.
![ATA 1.5 제거](http://i.imgur.com/x4nJycx.png)
3.  ATA 센터 v1.5를 다시 설치합니다. 이전 ATA 1.5 설치와 동일한 구성(인증서, IP 주소, DB 경로 등)을 사용해야 합니다.
4.  다음 서비스를 다음 순서대로 중지합니다.
    1.  Microsoft Advanced Threat Analytics Center
    2.  MongoDB
5.  MongoDB 데이터베이스 파일을 "data_old" 폴더의 파일로 바꿉니다.
6.  다음 서비스를 다음 순서대로 시작합니다.
    1.  MongoDB
    2.  Microsoft Advanced Threat Analytics Center
7.  로그를 검토하여 제품이 오류 없이 실행되고 있는지 확인합니다.
8.  "RemoveDuplicateProfiles.exe" 도구를 [다운로드](http://aka.ms/ataremoveduplicateprofiles "다운로드")하여 기본 설치 경로(%ProgramFiles%\Microsoft Advanced Threat Analytics\Center)에 복사합니다.
9.  관리자 권한 명령 프롬프트에서 “RemoveDuplicateProfiles.exe”를 실행하고 완료될 때까지 기다립니다.
10. …\Microsoft Advanced Threat Analytics\Center\MongoDB\bin 디렉터리: **Mongo ATA**에서 다음 명령을 입력합니다.

    db.SuspiciousActivities.remove({ "_t" : "RemoteExecutionSuspiciousActivity", "DetailsRecords" : { "$elemMatch" : { "ReturnCode" : null } } }, { "_id" : 1 });

![해결 방법 업데이트](http://i.imgur.com/Nj99X2f.png)

그러면 WriteResult({ "nRemoved" : XX })가 반환됩니다. 여기서 “XX”는 검색된 의심스러운 활동의 수입니다. 숫자가 0보다 큰 경우 명령 프롬프트를 종료하고 업데이트 프로세스를 계속 진행하세요.


### <a name="net-framework-461-requires-restarting-the-server"></a>Net Framework 4.6.1에서 서버 다시 시작 요구

경우에 따라 .Net Framework 4.6.1을 설치하면 서버를 다시 시작해야 할 수 있습니다. **Microsoft Advanced Threat Analytics Center 설치** 대화 상자에서 확인을 클릭하면 서버가 자동으로 다시 시작됩니다. 이 과정은 도메인 컨트롤러에 ATA 경량 게이트웨이를 설치할 때 특히 중요한데, 설치 전에 유지 관리 기간을 계획해야 하기 때문입니다.
    ![.NET Framework 다시 시작](media/ata-net-framework-restart.png)

### <a name="historical-network-activities-no-longer-migrated"></a>기록 네트워크 활동이 더 이상 마이그레이션되지 않음
이 버전의 ATA는 향상된 검색 엔진을 제공하여 보다 정확한 검색을 제공하고 특히 Pass-the-Hash에 대한 많은 가양성 시나리오를 줄여줍니다.
새롭고 향상된 검색 엔진은 인라인 검색 기술을 활용하여 기록 네트워크 활동에 액세스하지 않고 검색을 수행하므로 ATA 센터의 성능이 현저하게 향상됩니다. 또한 업데이트 절차 중에 기록 네트워크 활동을 마이그레이션할 필요도 없습니다.
ATA 업데이트 절차에서는 향후 조사를 위해 원하는 경우 데이터를 JSON 파일로 `<Center Installation Path>\Migration`에 내보냅니다.

## <a name="see-also"></a>참고 항목
[ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[버전 1.6으로 ATA 업데이트 - 마이그레이션 가이드](ata-update-1.6-migration-guide.md)


<!--HONumber=Nov16_HO3-->


