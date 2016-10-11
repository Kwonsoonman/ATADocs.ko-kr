---
title: "역할 그룹 작업 - 완료 | Microsoft ATA"
description: "ATA 역할 그룹 작업을 안내합니다."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 869d8f830d5dc70c927f172d77642b0c97bdcd84


---

*적용 대상: Advanced Threat Analytics 버전 1.7*




# ATA 역할 그룹

역할 그룹에서는 ATA에 대한 액세스 권한을 관리할 수 있습니다. 역할 그룹을 사용하여 보안 팀 내에서 업무를 구분할 수 있으며 사용자가 해당 작업을 수행할 때 필요한 액세스 권한만큼만 부여할 수도 있습니다. 이 문서는 액세스 관리 및 ATA 역할 권한 부여에 대해 설명하며, 사용자가 ATA의 역할 그룹을 사용하여 구동하고 실행하는 데 도움을 줍니다.
## ATA 역할 그룹 유형 

ATA에 3가지 유형의 역할 그룹(ATA Administrator, ATA Analyst 및 ATA Executive)이 도입되었습니다. 다음 표에서는 역할에 따라 사용할 수 있는 ATA의 액세스 유형에 대해 설명합니다. 할당하는 역할에 따라 다음과 같이 ATA의 다양한 화면과 메뉴 옵션을 사용할 수 있습니다.

|활동 |Microsoft Advanced Threat Analytics Administrator|Microsoft Advanced Threat Analytics Analyst|Microsoft Advanced Threat Analytics Executive|
|----|----|----|----|
|로그인|사용 가능|사용 가능|사용 가능|
|의심스러운 활동에 대한 입력 제공|사용 가능|사용 가능|사용할 수 없음|
|의심스러운 활동의 상태 변경|사용 가능|사용 가능|사용할 수 없음|
|전자 메일/가져오기 링크를 통해 의심스러운 활동 공유/내보내기|사용 가능|사용 가능|사용할 수 없음|
|의심스러운 활동에 대한 참고 사항 추가/편집|사용 가능|사용 가능|사용할 수 없음|
|모니터링 경고의 상태 변경|사용 가능|사용 가능|사용할 수 없음|
|ATA 구성 업데이트|사용 가능|사용할 수 없음|사용할 수 없음|
|게이트웨이 - 추가|사용 가능|사용할 수 없음|사용할 수 없음|
|게이트웨이 - 삭제 |사용 가능|사용할 수 없음|사용할 수 없음|
|모니터링된 DC – 추가 |사용 가능|사용할 수 없음|사용할 수 없음|
|모니터링된 DC – 삭제|사용 가능|사용할 수 없음|사용할 수 없음|

사용자가 자신의 역할 그룹으로 사용할 수 없는 페이지에 액세스하려고 하면 ATA의 권한 없음 페이지로 리디렉션됩니다. 

## 사용자 추가/제거 - ATA 역할 그룹 

ATA에서는 역할 그룹에 대한 기준으로 로컬 Windows 그룹을 사용합니다. 사용자를 추가하거나 제거하려면 **로컬 사용자 및 그룹** MMC(Lusrmgr.msc)를 사용하세요. 도메인에 가입된 컴퓨터에서 로컬 계정과 도메인 계정을 추가할 수 있습니다. 




<!--HONumber=Sep16_HO4-->


