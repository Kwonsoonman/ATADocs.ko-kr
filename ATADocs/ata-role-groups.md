---
title: "액세스 관리를 위한 Advanced Threat Analytics 역할 그룹 | Microsoft 문서"
description: "ATA 역할 그룹 작업을 안내합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 06f96ad4627cd5400d822caabeaff15dfaabfb72
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*




# <a name="ata-role-groups"></a>ATA 역할 그룹

역할 그룹에서는 ATA에 대한 액세스 권한을 관리할 수 있습니다. 역할 그룹을 사용하여 보안 팀 내에서 업무를 구분할 수 있으며 사용자가 해당 작업을 수행할 때 필요한 액세스 권한만큼만 부여할 수도 있습니다. 이 문서는 액세스 관리 및 ATA 역할 권한 부여에 대해 설명하며, 사용자가 ATA의 역할 그룹을 사용하여 구동하고 실행하는 데 도움을 줍니다.

> [!NOTE]
> ATA 센터의 모든 로컬 관리자는 자동으로 Microsoft Advanced Threat Analytics 관리자가 됩니다.

## <a name="types-of-ata-role-groups"></a>ATA 역할 그룹 유형 

ATA에서는 세 가지 유형의 역할 그룹, ATA 관리자, ATA 사용자 및 ATA 뷰어를 소개합니다. 다음 표에서는 역할에 따라 사용할 수 있는 ATA의 액세스 유형에 대해 설명합니다. 할당하는 역할에 따라 다음과 같이 ATA의 다양한 화면과 메뉴 옵션을 사용할 수 있습니다.

|활동 |Microsoft Advanced Threat Analytics 관리자|Microsoft Advanced Threat Analytics 사용자|Microsoft Advanced Threat Analytics 뷰어|
|----|----|----|----|
|로그인|사용 가능|사용 가능|사용 가능|
|의심스러운 활동에 대한 입력 제공|사용 가능|사용 가능|사용할 수 없음|
|의심스러운 활동의 상태 변경|사용 가능|사용 가능|사용할 수 없음|
|전자 메일/가져오기 링크를 통해 의심스러운 활동 공유/내보내기|사용 가능|사용 가능|사용할 수 없음|
|모니터링 경고의 상태 변경|사용 가능|사용 가능|사용할 수 없음|
|ATA 구성 업데이트|사용 가능|사용할 수 없음|사용할 수 없음|
|게이트웨이 - 추가|사용 가능|사용할 수 없음|사용할 수 없음|
|게이트웨이 - 삭제 |사용 가능|사용할 수 없음|사용할 수 없음|
|모니터링된 DC – 추가 |사용 가능|사용할 수 없음|사용할 수 없음|
|모니터링된 DC – 삭제|사용 가능|사용할 수 없음|사용할 수 없음|
|경고 및 의심스러운 활동 보기|사용 가능|사용 가능|사용 가능|


사용자가 자신의 역할 그룹으로 사용할 수 없는 페이지에 액세스하려고 하면 ATA의 권한 없음 페이지로 리디렉션됩니다. 

## <a name="add--remove-users---ata-role-groups"></a>사용자 추가/제거 - ATA 역할 그룹 

ATA에서는 역할 그룹에 대한 기준으로 로컬 Windows 그룹을 사용합니다. 역할 그룹은 ATA 센터 서버에서 관리되어야 합니다.
사용자를 추가하거나 제거하려면 **로컬 사용자 및 그룹** MMC(Lusrmgr.msc)를 사용하세요. 도메인에 가입된 컴퓨터에서 로컬 계정과 도메인 계정을 추가할 수 있습니다. 

