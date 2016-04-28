---
# required metadata

title: ATA 검색 설정 작업 | Microsoft Advanced Threat Analytics
description: 일반적이지 않은 상황에 사용되고 네트워크의 다른 엔터티와 다르게 처리해야 하는 IP 주소 및 서브넷 목록을 구성하는 방법을 설명합니다.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 검색 설정 작업
**검색** 구성 페이지에서 일반적이지 않은 상황에 사용되고 네트워크의 다른 엔터티와 약간 다르게 처리해야 하는 IP 주소 및 서브넷 목록을 설정할 수 있습니다.

## 검색 설정
**검색** 페이지에서 다음 항목을 정의할 수 있습니다.

-   **단기 임대 서브넷** - 조직에 IP 주소가 매우 단기적인 서브넷(예: VPN IP 주소 서브넷 또는 Wi-Fi 서브넷)이 있는 경우 ATA에 이러한 IP 주소 및 서브넷을 입력해야 합니다. 그래야 ATA에서 다른 IP 주소와 달리 이러한 범위의 IP 주소와 컴퓨터 간의 연결을 보다 짧은 기간 동안 저장합니다.

-   **허니토큰 계정 SID** – 네트워크 활동이 없어야 하는 사용자 계정입니다. 이 계정은 ATA 허니토큰 사용자로 구성됩니다. 다른 사람이 이 사용자 계정을 사용하려고 시도하는 경우 ATA에서 의심스러운 활동을 만들고 악의적인 활동을 표시합니다. 허니토큰 사용자를 구성하려면 사용자 이름이 아니라 사용자 계정의 SID가 필요합니다.

다음 검색에서 IP 주소를 제외할 수 있습니다. 이러한 목록 중 하나에 IP 주소를 입력한 경우 ATA는 해당 IP 주소를 이 특정 유형의 검색된 활동에서 제외합니다.

-   DNS 정찰 IP 주소 제외

-   Pass-the-Ticket IP 주소 제외

## 참고 항목
- [의심스러운 활동 작업](working-with-suspicious-activities.md)
- [ATA 구성 수정](modifying-ata-configuration.md)
- [지원이 필요한 경우 포럼을 확인하세요.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


