---
title: "고급 위협 분석의 검색에서 엔터티 제외 | Microsoft Docs"
description: "ATA가 특정 엔터티 활동을 의심스러운 것으로 검색하지 못 하게 하는 방법에 관해 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/9/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ff60b026c754a27da62c01ce6c551d206338ef4e
ms.sourcegitcommit: be6bdfa24a9b25a3375a4768d513b93900b3a498
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# 검색에서 엔터티 제외
<a id="excluding-entities-from-detections" class="xliff"></a>
이 항목에서는 무해한 참 긍정을 최소화면서도 참 긍정을 파악하도록 트리거되는 경고에서 엔터티를 제외하는 방법에 관해 설명합니다. 특정 사용자에게 ATA가 일상적인 비즈니스 리듬의 일부가 될 수 있는 활동에 대해 불필요한 잡음이 되지 않도록 발생하는 경고에서 특정 엔터티를 최소화하거나 제외할 수 있습니다.

예를 들어 DNS 정찰을 수행하는 보안 스캐너이거나 도메인 컨트롤러에서 원격으로 스크립트를 실행하는 관리자인 경우, 이러한 사용 권한 활동은 조직의 일반적인 IT 작업의 일부로 사용됩니다.

ATA에 발생하는 경고에서 엔터티를 제외하려면:

의심스러운 활동 자체에서 제외하거나 **구성** 페이지의 **제외** 탭에서 엔터티를 제외할 수 있습니다.

- **의심스러운 활동에서 제외**: 의심스러운 활동 타임라인에서 특정 활동을 수행하도록 허용된 사용자 또는 컴퓨터나 IP 주소의 활동에 대한 경고가 자주 나타나는 경우, 해당 엔터티에서 의심스러운 활동이 있는 행 끝에 세 점을 오른쪽 마우스로 클릭하고 **닫기 및 제외**를 선택합니다. <br></br>그러면 사용자, 컴퓨터 또는 IP 주소가 의심스러운 해당 활동에 대한 제외 목록에 추가됩니다. 의심스러운 활동도 닫히게 되며 **의심스러운 활동 타임라인**의 **열기** 이벤트 목록에 더 이상 나열되지 않습니다.

    ![엔터티 제외](./media/exclude-in-sa.png)

- **구성 페이지에서 제외**: 설정한 모든 제외를 검토하거나 수정하려면 **구성**에서 **제외**를 클릭한 다음 **표시된 중요한 계정 자격 증명**과 같은 의심스러운 활동을 선택합니다.

    ![제외 구성](./media/exclusions-config-page.png)

**제외** 구성에서 엔터티 제거: 엔터티 이름 옆의 빼기를 클릭한 다음 페이지 하단의 **저장**을 클릭합니다.

유형에 대한 경고가 나타나면 무해한 참 긍정인지 확인한 다음에 제외를 검색에 추가하는 것이 좋습니다. 

> [!NOTE]
> 보호를 위해 모든 검색이 제외를 설정할 수 있는 것은 아닙니다. 

일부 검색에서는 제외할 항목을 결정하는 데 도움이 되는 팁을 제공합니다. 

각 제외는 컨텍스트에 따라 다르며 일부는 사용자를 사용할 수 있고 나머지는 컴퓨터 또는 IP 주소를 설정할 수 있습니다. 

IP 주소 또는 컴퓨터를 제외할 수 있는 경우 둘 중 하나만 제외할 수 있으며 모두 제공할 필요는 없습니다.

> [!NOTE]
> ATA 관리자만 구성 페이지를 수정할 수 있습니다.


## 참고 항목
<a id="see-also" class="xliff"></a>
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [ATA 구성 수정](modifying-ata-center-configuration.md)
