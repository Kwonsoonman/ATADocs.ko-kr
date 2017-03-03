---
title: "Advanced Threat Analytics 검색 설정 | Microsoft 문서"
description: "일반적이지 않은 상황에 사용되고 네트워크의 다른 엔터티와 다르게 처리해야 하는 IP 주소 및 서브넷 목록을 구성하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: c88d74793c6210704f2a187df6508bf525907118


---

*적용 대상: Advanced Threat Analytics 버전 1.7*



# <a name="working-with-ata-detection-settings"></a>ATA 검색 설정 작업
**검색** 구성 페이지에서 일반적이지 않은 상황에 사용되고 네트워크의 다른 엔터티와 약간 다르게 처리해야 하는 IP 주소 및 서브넷 목록을 설정할 수 있습니다.

## <a name="setting-up-detection"></a>검색 설정
**검색** 섹션에서 다음 항목을 정의할 수 있습니다.

-   **허니토큰 계정 SID** – 네트워크 활동이 없어야 하는 사용자 계정입니다. 이 계정은 ATA 허니토큰 사용자로 구성됩니다. 다른 사람이 이 사용자 계정을 사용하려고 시도하는 경우 ATA에서 의심스러운 활동을 만들고 악의적인 활동을 표시합니다. 허니토큰 사용자를 구성하려면 사용자 이름이 아니라 사용자 계정의 SID가 필요합니다.

>[!NOTE]
> 사용자의 SID는 ATA 콘솔에서 사용자 계정의 *계정 정보* 탭에서 확인할 수 있습니다.


![ATA 검색 설정 허니토큰](media/ata-detection-settings-honeytoken-1.7.png)


**검색 제외** - 다음 검색에서 IP 주소를 제외할 수 있습니다. 이러한 목록 중 하나에 IP 주소를 입력한 경우 ATA는 해당 IP 주소를 이 특정 유형의 검색된 활동에서 제외합니다.

-   DNS 정찰 IP 주소 제외

-   Pass-the-Ticket IP 주소 제외

![ATA 검색 설정 제외](media/ata-detection-settings-exclusions-1.7.png)


## <a name="see-also"></a>참고 항목
- [의심스러운 활동 작업](working-with-suspicious-activities.md)
- [ATA 구성 수정](modifying-ata-configuration.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


