---
title: "ATA 로그를 사용하여 ATA 문제 해결 | Microsoft ATA"
description: "ATA 로그를 사용하여 문제를 해결하는 방법을 설명합니다."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b8ad5511-8893-4d1d-81ee-b9a86e378347
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: f13b448399f4184ebb110883800e87902d3b7ac3


---

# ATA 로그를 사용하여 ATA 문제 해결
ATA 로그는 ATA의 각 구성 요소가 주어진 시점에 수행하는 작업을 이해할 수 있도록 도와줍니다.

## ATA 게이트웨이 로그
이 섹션에서는 ATA 게이트웨이에 대한 모든 참조가 ATA 경량 게이트웨이와도 관련됩니다. 

ATA 게이트웨이 로그는 **Logs**라는 하위 폴더에 있습니다. 기본 설치 위치에서는 **C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs**에서 찾을 수 있습니다.

ATA 게이트웨이에는 다음 로그가 있습니다.

-   **Microsoft.Tri.Gateway.log** - 이 로그에는 ATA 게이트웨이에서 발생하는 모든 항목(해결 방법 및 오류 포함)이 포함되어 있습니다. 기본 사용: 모든 작업의 전체적인 상태를 발생한 시간 순서대로 가져옵니다.

-   **Microsoft.Tri.Gateway-Resolution.log** - 이 로그에는 ATA 게이트웨이에 의해 트래픽에서 확인된 엔터티의 확인 정보가 포함됩니다. 기본 사용: 엔터티 확인 문제를 조사합니다.

-   **Microsoft.Tri.Gateway-Errors.log** – 이 로그는 ATA 게이트웨이에서 발생한 오류만 포함합니다. 기본 사용: 상태 검사를 수행하고 특정 시간과 상호 연결해야 하는 문제를 조사합니다.

-   **Microsoft.Tri.Gateway-ExceptionStatistics.log** – 이 로그는 유사한 모든 오류 및 예외를 그룹화하고 개수를 측정합니다.
    이 파일은 ATA 게이트웨이 서비스가 시작될 때마다 빈 상태로 시작한 후 1분 간격으로 업데이트됩니다. 기본 사용: ATA 게이트웨이와 관련해서 새로운 오류나 문제가 있는지 파악합니다. 오류가 보다 읽기 쉽게 그룹화되며 새로운 유형의 오류나 문제가 있는지 쉽게 파악할 수 있습니다.

> [!NOTE]
> 처음 세 개의 로그 파일에 최대 50MB까지 할당됩니다. 이 크기에 도달하면 새 로그 파일이 열리고 이전 로그 파일의 이름은 "&lt;원래 파일 이름&gt;-Archived-00000"으로 바뀝니다. 여기서 번호는 이름이 바뀔 때마다 커집니다.

## ATA 센터 로그
ATA 센터 로그는 **Logs**라는 하위 폴더에 있습니다. 기본 설치 위치에서는 **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs**에서 찾을 수 있습니다.

ATA 센터에는 다음 로그가 있습니다.

-   **Microsoft.Tri.Center.log** – 이 로그에는 ATA 센터에서 발생하는 모든 항목(검색 내용 및 오류 포함)이 포함되어 있습니다. 기본 사용: 모든 작업의 전체적인 상태를 발생한 시간 순서대로 가져옵니다.

-   **Microsoft.Tri.Center-Detection.log** – 이 로그는 ATA 센터의 검색 세부 정보만 포함합니다. 기본 사용: 검색 문제를 조사합니다.

-   **Microsoft.Tri.Center-Errors.log** – 이 로그는 ATA 센터에서 발생한 오류만 포함합니다. 기본 사용: 상태 검사를 수행하고 특정 시간과 상호 연결해야 하는 문제를 조사합니다.

-   **Microsoft.Tri.Center-ExceptionStatistics.log** – 이 로그는 유사한 모든 오류 및 예외를 그룹화하고 개수를 측정합니다.
    이 파일은 ATA 센터 서비스가 시작될 때마다 빈 상태로 시작한 후 1분 간격으로 업데이트됩니다. 기본 사용: ATA 센터와 관련해서 새로운 오류나 문제가 있는지 파악합니다. 오류가 보다 읽기 쉽게 그룹화되며 새로운 유형의 오류나 문제가 있는지 쉽게 파악할 수 있습니다.

> [!NOTE]
> 처음 세 개의 로그 파일에 최대 50MB까지 할당됩니다. 이 크기에 도달하면 새 로그 파일이 열리고 이전 로그 파일의 이름은 "&lt;원래 파일 이름&gt;-Archived-00000"으로 바뀝니다. 여기서 번호는 이름이 바뀔 때마다 커집니다.

## ATA 콘솔 로그
ATA 콘솔 로그(관리 API 로그)는 **Logs**라는 하위 폴더에 있습니다. 기본 설치 위치에서는 **C:\Program Files\Microsoft Advanced Threat Analytics\Center\Management\Logs**에서 찾을 수 있습니다.

ATA 콘솔에는 다음 로그가 있습니다.

-   **w3wp.log** – 이 로그에는 관리 프로세스(IIS)에서 발생하는 모든 문제가 포함됩니다.


-   **w3wp-Errors.log** – 이 로그는 관리 프로세스(IIS)에서 발생한 오류만 포함합니다.


-   **8e75f9f1-ExceptionStatistics.log** – 이 로그는 유사한 모든 오류 및 예외를 그룹화하고 개수를 측정합니다.
    이 파일은 게이트웨이 서비스가 시작될 때마다 빈 상태로 시작한 후 1분 간격으로 업데이트됩니다. 기본 사용: ATA 센터와 관련해서 새로운 오류나 문제가 있는지 파악합니다. 오류가 보다 읽기 쉽게 그룹화되며 새로운 유형의 오류나 문제가 있는지 쉽게 파악할 수 있습니다.

> [!NOTE]
> 처음 두 개의 로그 파일에 최대 50MB까지 할당됩니다. 이 크기에 도달하면 새 로그 파일이 열리고 이전 로그 파일의 이름은 "&lt;원래 파일 이름&gt;-Archived-00000"으로 바뀝니다. 여기서 번호는 이름이 바뀔 때마다 커집니다.

## ATA 배포 로그
ATA 배포 로그는 제품을 설치한 사용자에 대한 임시 디렉터리에 있습니다. 기본 설치 위치에서는 **C:\Users\Administrator\AppData\Local\Temp**(또는 %temp% 위의 디렉터리)에서 찾을 수 있습니다.

ATA 센터 배포 로그:

-   **Microsoft Advanced Threat Analytics Center_20150601104213.log** - 이 로그는 ATA 센터의 배포 프로세스에 포함된 단계를 나열합니다. 기본 사용: ATA 센터 배포 프로세스를 추적합니다.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_0_MongoDBPackage.log** - 이 로그는 ATA 센터의 MongoDB 배포 프로세스에 포함된 단계를 나열합니다. 기본 사용: MongoDB 배포 프로세스를 추적합니다.

-   **Microsoft Advanced Threat Analytics Center_20150601104213_1_MsiPackage.log** - 이 로그 파일은 ATA 센터 이진 파일의 배포 프로세스에 포함된 단계를 나열합니다. 기본 사용: ATA 센터 이진 파일의 배포를 추적합니다.

ATA 게이트웨이 및 ATA 경량 게이트웨이 배포 로그:

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801.log** - 이 로그는 ATA 게이트웨이의 배포 프로세스에 포함된 단계를 나열합니다. 기본 사용: ATA 게이트웨이 배포 프로세스를 추적합니다.

-   **Microsoft Advanced Threat Analytics Gateway_20151214014801_001_MsiPackage.log** - 이 로그는 ATA 게이트웨이 이진 파일의 배포 프로세스에 포함된 단계를 나열합니다. 기본 사용: ATA 게이트웨이 이진 파일의 배포를 추적합니다.

## 참고 항목
- [ATA 필수 구성 요소](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 용량 계획](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [이벤트 수집 구성](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Windows 이벤트 전달 구성](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


