---
title: "ATA 버전 1.4의 새로운 기능 | Microsoft ATA"
description: "알려진 문제와 함께 ATA 버전 1.4의 새로운 기능을 나열합니다."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: cbea47f9-34c1-42b6-ae9e-6a472b49e1a5
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: b66a315c9a98192cbd3b6feea462445c085091b1


---

# ATA 버전 1.4의 새로운 기능
이 릴리스 정보에서는 버전 1.4의 Advanced Threat Analytics에서 알려진 문제에 대한 정보를 제공합니다.

## 이 버전의 새로운 기능

-   도메인 컨트롤러에서 ATA Gateway로 이벤트를 직접 보내는 WEF(Windows Event Forwarding) 지원

-   DPI(심층 패킷 검사)와 Windows 이벤트 로그를 결합하여 회사 리소스에 대한 향상된 Pass-The-Hash 검색 기능

-   도메인에 가입되지 않은 장치와 Windows가 아닌 장치에 대한 검색 및 표시 유형 지원 향상

-   ATA Gateway당 더 많은 트래픽을 지원하는 성능 향상

-   ATA Center당 더 많은 ATA Gateway를 지원하는 성능 향상

-   컴퓨터 이름 및 IP를 일치시키는 새 자동 이름 확인 프로세스 추가 - 이 고유한 기능은 조사 프로세스 시간을 단축하고 보안 분석가를 위한 강력한 증거를 제공함

-   사용자 입력을 수집하여 검색 프로세스를 자동으로 세밀하게 조정하는 기능 향상

-   NAT 장치에 대한 자동 검색

-   도메인 컨트롤러에 연결할 수 없는 경우 자동 장애 조치(failover)

-   배포의 전반적인 상태와 구성 및 연결 관련 문제를 제공하는 시스템 상태 모니터링 및 알림

-   엔터티가 작동하는 사이트 및 위치에 대한 가시성

-   다중 도메인 지원

-   SLD(단일 레이블 도메인) 지원

-   ATA Gateway 및 ATA Center의 IP 주소와 인증서 수정 지원

-   고객 환경을 개선하기 위한 문제 해결

## 알려진 문제
이 버전에는 다음과 같은 알려진 문제가 존재합니다.

### 네트워크 캡처 소프트웨어
ATA 게이트웨이에서 설치할 수 있는 네트워크 캡처 소프트웨어는 [Microsoft 네트워크 모니터 3.4](http://www.microsoft.com/download/details.aspx?id=4865)만 지원됩니다. Microsoft 메시지 분석기 또는 다른 네트워크 캡처 소프트웨어를 설치하지 마세요. 다른 소프트웨어를 설치하면 ATA Gateway 작동이 중지됩니다.

### Zip 파일에서 설치
ATA Gateway를 설치할 때 zip 파일에서 로컬 디렉터리에 파일을 추출하고 해당 디렉터리에서 설치해야 합니다. Zip 파일 내에서 직접 ATA Gateway를 설치하지 마세요. 설치가 실패합니다.

### 이전 버전의 ATA 제거
이전 버전의 ATA, 공개 미리 보기 또는 비공개 미리 보기 버전을 설치한 경우 이 릴리스의 ATA를 설치하기 전에 ATA Center 및 ATA Gateway를 제거해야 합니다.

또한 데이터베이스 파일과 로그 파일을 삭제해야 합니다. ATA 이전 버전의 데이터베이스는 ATA GA 버전과 호환되지 않습니다.

ATA Center 또는 ATA Gateway를 제거할 때 제거 대신 ATA 설치가 열리는 경우 다음 레지스트리 키를 추가한 다음 ATA를 다시 제거해야 합니다.

**ATA Center**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center

-   값이 `C:\Program Files\Microsoft Advanced Threat Analytics\Center`인 `InstallationPath`라는 새 문자열 값을 추가합니다. 이는 기본 설치 폴더입니다. 설치 폴더를 변경한 경우 ATA가 설치된 경로를 입력합니다.

    ![ATA Center 설치 경로에 대한 레지스트리 편집기](media/ATA-uninstall-center-bug.jpg)

**ATA Gateway**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Gateway

-   값이 `C:\Program Files\Microsoft Advanced Threat Analytics\Gateway`인 `InstallationPath`라는 새 문자열 값을 추가합니다. 이는 기본 설치 폴더입니다.  설치 폴더를 변경한 경우 ATA가 설치된 경로를 입력합니다.

    ![ATA Gateway 설치 경로에 대한 레지스트리 편집기](media/ATA-GW-uninstall-bug.jpg)

제거 후 ATA Center와 ATA Gateway 둘 다에서 설치 폴더를 삭제합니다.  별도 폴더에 데이터베이스를 설치한 경우 ATA Center에서 데이터베이스 폴더를 삭제합니다.

### 상태 경고 - 연결이 끊긴 ATA Gateway
둘 이상의 ATA Gateway가 있고 연결이 끊긴 ATA Gateway 경고가 나타나는 경우 둘 중 하나에서만 자동 해결이 작동하고 나머지는 미해결 상태로 유지됩니다. ATA Gateway가 가동되고 서비스가 실행 중인지 수동으로 확인하여 경고를 수동으로 해결해야 합니다.

### 가상화 호스트의 KB
가상화 호스트에 KB 3047154를 설치하지 마세요. 포트 미러링이 제대로 작동하지 않을 수 있습니다.

## 참고 항목

[버전 1.6으로 ATA 업데이트 - 마이그레이션 가이드](ata-update-1.6-migration-guide.md)

[ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)


<!--HONumber=Jul16_HO4-->


