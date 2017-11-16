---
title: "Advanced Threat Analytics 배포 시 포트 미러링 구성 | Microsoft 문서"
description: "포트 미러링 옵션과 ATA에 대해 이러한 옵션을 구성하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: fb9c6aa3962f7fc121f3737a32c9a5cfb2fcfb8e
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="configure-port-mirroring"></a>포트 미러링 구성
> [!NOTE] 
> 이 문서는 ATA 경량 게이트웨이 대신 ATA 게이트웨이를 배포하는 경우에만 해당합니다. ATA 게이트웨이를 사용해야 하는지 확인하려면 [배포에 사용할 올바른 게이트웨이 선택](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment)을 참조하세요.
 
ATA에서 사용되는 기본 데이터 원본은 도메인 컨트롤러로 들어오고 나가는 네트워크 트래픽의 상세한 패킷 검사입니다. ATA에서 네트워크 트래픽을 보려면 포트 미러링을 구성하거나 네트워크 TAP를 사용해야 합니다.

포트 미러링의 경우 각 도메인 컨트롤러에서 미러링할 **포트 미러링**을 네트워크 트래픽의 **원본**으로 구성합니다. 일반적으로는 네트워킹 또는 가상화 팀과 협의하여 포트 미러링을 구성해야 합니다.
자세한 내용은 공급업체의 설명서를 참조하세요.

도메인 컨트롤러와 ATA Gateway는 물리적이거나 가상일 수 있습니다. 다음은 일반적인 포트 미러링 방법과 몇 가지 고려 사항입니다. 자세한 내용은 스위치 또는 가상화 서버 제품 설명서를 참조하세요. 스위치 제조업체에서는 다른 용어를 사용할 수도 있습니다.

**SPAN(Switched Port Analyzer)** – 하나 이상의 스위치 포트에서 같은 스위치에 있는 다른 스위치 포트로 네트워크 트래픽을 복사합니다. ATA Gateway와 도메인 컨트롤러 둘 다 동일한 물리적 스위치에 연결되어야 합니다.

**RSPAN(Remote Switch Port Analyzer)**  – 여러 물리적 스위치를 통해 분산된 원본 포트의 네트워크 트래픽을 모니터링할 수 있습니다. RSPAN은 원본 트래픽을 특정 RSPAN 구성 VLAN에 복사합니다. 이 VLAN은 포함된 다른 스위치에 트렁크되어야 합니다. RSPAN은 계층 2에서 작동합니다.

**ERSPAN(Encapsulated Remote Switch Port Analyzer)** – 계층 3에서 작동하는 Cisco 소유 기술입니다. ERSPAN을 사용하면 VLAN 트렁크 없이 스위치 간의 트래픽을 모니터링할 수 있습니다. ERSPAN은 GRE(Generic Routing Encapsulation)를 사용하여 모니터링되는 네트워크 트래픽을 복사합니다. 현재 ATA는 ERSPAN 트래픽을 직접 받을 수 없습니다. ATA가 ERSPAN 트래픽과 함께 작동하려면 트래픽의 캡슐화를 해제할 수 있는 스위치 또는 라우터를 트래픽의 캡슐화를 해제할 ERSPAN의 대상으로 구성해야 합니다. 그런 다음 SPAN 또는 RSPAN을 사용하여 캡슐화가 해제된 트래픽을 ATA 게이트웨이로 전달하도록 스위치 또는 라우터를 구성해야 합니다.

> [!NOTE]
> 포트 미러링되는 도메인 컨트롤러가 WAN 링크를 통해 연결된 경우 WAN 링크에서 ERSPAN 트래픽의 추가 부하를 처리할 수 있는지 확인합니다.
> ATA는 트래픽이 같은 방식으로 NIC 및 도메인 컨트롤러에 도달하는 경우에만 트래픽 모니터링을 지원합니다. ATA는 트래픽이 서로 다른 포트로 분산되는 경우 트래픽 모니터링을 지원하지 않습니다.

## <a name="supported-port-mirroring-options"></a>지원되는 포트 미러링 옵션

|ATA Gateway|도메인 컨트롤러|고려 사항|
|---------------|---------------------|------------------|
|가상|같은 호스트의 가상|가상 스위치가 포트 미러링을 지원해야 합니다.<br /><br />자체적으로 가상 컴퓨터 중 하나를 다른 호스트로 이동하면 포트 미러링이 중단될 수 있습니다.|
|가상|다른 호스트의 가상|가상 스위치가 이 시나리오를 지원해야 합니다.|
|가상|물리적|전용 네트워크 어댑터가 필요합니다. 그렇지 않으면 ATA Center로 전송되는 트래픽을 포함하여 호스트에서 들어오고 나가는 모든 트래픽이 ATA에 표시됩니다.|
|물리적|가상|가상 스위치가 이 시나리오를 지원하고 시나리오에 따라 물리적 스위치의 포트 미러링 구성을 지원해야 합니다.<br /><br />가상 호스트가 동일한 물리적 스위치에 있는 경우 스위치 수준 범위를 구성해야 합니다.<br /><br />가상 호스트가 다른 스위치에 있는 경우 RSPAN 또는 ERSPAN&#42;을 구성해야 합니다.|
|물리적|같은 스위치의 물리적|물리적 스위치가 SPAN/포트 미러링을 지원해야 합니다.|
|물리적|다른 스위치의 물리적|물리적 스위치가 RSPAN 또는 ERSPAN&#42;을 지원해야 합니다.|
&#42; ERSPAN은 ATA에서 트래픽을 분석하기 전에 캡슐화 해제가 수행되는 경우에만 지원됩니다.

> [!NOTE]
> 도메인 컨트롤러와 여기에 연결되는 ATA 게이트웨이의 시간이 서로 5분 이내에 동기화되어야 합니다.

**가상화 클러스터를 사용하는 경우**

-   ATA Gateway가 있는 가상 컴퓨터의 가상화 클러스터에서 실행 중인 각 도메인 컨트롤러에 대해 도메인 컨트롤러와 ATA Gateway 간의 선호도를 구성합니다. 그러면 도메인 컨트롤러가 클러스터의 다른 호스트로 이동되는 경우 ATA 게이트웨이가 따라서 이동합니다. 이는 소수의 도메인 컨트롤러가 있는 경우에 적합합니다.
> [!NOTE]
> 사용자 환경이 다른 호스트의 V2V(RSPAN)를 지원하는 경우 선호도에 대해 걱정할 필요가 없습니다.
> 
-   ATA Gateway가 모든 DC 모니터링을 자체적으로 처리하기에 적절한 크기로 설정되었는지 확인하려면 각 가상화 호스트에 가상 컴퓨터를 설치하고 각 호스트에 ATA Gateway를 설치합니다. 클러스터에서 실행되는 모든 도메인 컨트롤러를 모니터링하도록 각 ATA Gateway를 구성합니다. 그러면 도메인 컨트롤러가 실행되는 모든 호스트가 모니터링됩니다.

포트 미러링을 구성한 후에는 ATA Gateway를 설치하기 전에 포트 미러링이 작동하는지 확인합니다.

## <a name="see-also"></a>참고 항목
- [포트 미러링 유효성 검사](validate-port-mirroring.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
