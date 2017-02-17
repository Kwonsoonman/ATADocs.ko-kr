---
title: "Advanced Threat Analytics 버전 1.5의 새로운 기능 | Microsoft 문서"
description: "알려진 문제와 함께 ATA 버전 1.5의 새로운 기능을 나열합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 08da33114bc3f0c9aafb9914b9d77a88fac009f4


---

# <a name="whats-new-in-ata-version-15"></a>ATA 버전 1.5의 새로운 기능
이 릴리스 정보에서는 이 버전의 Advanced Threat Analytics에서 알려진 문제에 대한 정보를 제공합니다.

## <a name="whats-new-in-the-ata-15-update"></a>ATA 1.5 업데이트의 새로운 기능
ATA 1.5 업데이트에서는 다음 영역에 대한 향상된 기능을 제공합니다.

-   검색 시간 단축

-   NAT(Network Address Translation) 장치용으로 향상된 자동 검색 알고리즘 제공

-   도메인에 가입되지 않은 장치용으로 향상된 이름 확인 프로세스 제공

-   제품 업데이트 중에 데이터 마이그레이션 지원

-   수천 개의 엔터티를 사용하여 의심스러운 활동에 대한 UI 응답성 향상

-   모니터링 경고의 자동 해결 기능 개선

-   모니터링 및 문제 해결 기능 향상을 위한 추가 성능 모니터 제공

## <a name="known-issues"></a>알려진 문제
이 버전에는 다음과 같은 알려진 문제가 존재합니다.

### <a name="new-ata-gateway-installation-fails"></a>새 ATA Gateway 설치 실패
ATA 배포를 ATA 버전 1.5로 업데이트한 후 새 ATA 게이트웨이를 설치하면 Microsoft Advanced Threat Analytics Gateway is not installed(Microsoft Advanced Threat Analytics 게이트웨이가 설치되어 있지 않습니다.)라는 오류가 표시됩니다.

![ATA GW 오류](media/ata-install-error.png)

<b>해결 방법:</b> <ataeval@microsoft.com>으로 전자 메일을 보내 문제 해결 단계를 요청합니다.
### <a name="deployment"></a>배포
"데이터베이스 데이터 경로" 및 "데이터베이스 저널 경로"에 대해 지정된 폴더는 비어 있어야 합니다(파일 또는 하위 폴더가 없어야 함).
비어 있지 않으면 배포가 진행되지 됩니다.

### <a name="installation-from-zip-file"></a>Zip 파일에서 설치
ATA Gateway를 설치할 때 zip 파일에서 로컬 디렉터리에 파일을 추출하고 해당 디렉터리에서 설치해야 합니다. Zip 파일 내에서 직접 ATA Gateway를 설치하지 마세요. 설치가 실패합니다.

### <a name="configuration"></a>구성
ATA Gateway 구성을 설정한 후 ATA Gateway를 처음 시작할 경우 서비스가 완전히 시작될 때까지(서비스를 처음 시작할 때 최대 10분이 걸릴 수 있음) "동기화되지 않음" 레이블이 표시됩니다.

### <a name="network-capture-software"></a>네트워크 캡처 소프트웨어
ATA 게이트웨이에서 설치할 수 있는 네트워크 캡처 소프트웨어는 [Microsoft 네트워크 모니터 3.4](http://www.microsoft.com/download/details.aspx?id=4865)만 지원됩니다. Microsoft 메시지 분석기 또는 다른 네트워크 캡처 소프트웨어를 설치하지 마세요. 다른 소프트웨어를 설치하면 ATA Gateway 작동이 중지됩니다.

### <a name="kb-on-virtualization-host"></a>가상화 호스트의 KB
가상화 호스트에 KB 3047154를 설치하지 마세요. 포트 미러링이 제대로 작동하지 않을 수 있습니다.

## <a name="see-also"></a>참고 항목

[버전 1.5로 ATA 업데이트 - 마이그레이션 가이드](ata-update-1.5-migration-guide.md)

[버전 1.6으로 ATA 업데이트 - 마이그레이션 가이드](ata-update-1.6-migration-guide.md)

[ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


