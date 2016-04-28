---
# required metadata

title: 포트 미러링 유효성 검사 | Microsoft Advanced Threat Analytics
description: 포트 미러링이 올바르게 구성되었는지 확인하는 방법을 설명합니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 포트 미러링 유효성 검사
다음 단계에서는 포트 미러링이 올바르게 구성되었는지 확인하는 프로세스를 안내합니다. ATA가 제대로 작동하려면 ATA Gateway에서 도메인 컨트롤러로 들어오고 나가는 트래픽을 볼 수 있어야 합니다. ATA에서 사용되는 기본 데이터 원본은 도메인 컨트롤러로 들어오고 나가는 네트워크 트래픽의 상세한 패킷 검사입니다. ATA에서 네트워크 트래픽을 보려면 포트 미러링을 구성해야 합니다. 포트 미러링은 하나의 포트(원본 포트)에서 다른 포트(대상 포트)로 트래픽을 복사합니다.

1.  [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) 또는 다른 네트워크 검색 도구를 설치합니다.

    > [!IMPORTANT]
    > Microsoft 메시지 분석기 또는 기타 네트워크 캡처 소프트웨어를 ATA Gateway에 설치하지 마세요.

2.  네트워크 모니터를 열고 새 캡처 탭을 만듭니다.

    1.  **캡처** 네트워크 어댑터 또는 포트 미러링 대상으로 구성된 스위치 포트에 연결된 네트워크 어댑터만 선택합니다.

    2.  P 모드가 설정되어 있는지 확인합니다.

    3.  **새 캡처**를 클릭합니다.

        ![새 캡처 탭 만들기 이미지](media/ATA-Port-Mirroring-Capture.jpg)

3.  표시 필터 창에서 **KerberosV5 또는 LDAP** 필터를 입력하고 **적용**을 클릭합니다.

    ![KerberosV5 또는 LDAP 필터 적용 이미지](media/ATA-Port-Mirroring-filter-settings.jpg)

4.  **시작**을 클릭하여 캡처 세션을 시작합니다. 도메인 컨트롤러로 들어오고 나가는 트래픽이 보이지 않는 경우 포트 미러링 구성을 검토합니다.

    > [!NOTE]
    > 도메인 컨트롤러로 들어오고 나가는 트래픽이 보이지는 확인해야 합니다.
    >
    > ![캡처 세션 시작 이미지](media/ATA-Port-Mirroring-Capture-traffic.jpg)

5.  한 방향의 트래픽만 보이는 경우 네트워킹 또는 가상화 팀과 함께 포트 미러링 구성 문제를 해결해야 합니다.

## 참고 항목

- [포트 미러링 구성](configure-port-mirroring.md)
- [지원이 필요한 경우 포럼을 확인하세요.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


