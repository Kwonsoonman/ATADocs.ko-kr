---
title: "ATA 구성 변경 - ATA 콘솔 IP 주소 | Microsoft Advanced Threat Analytics"
description: "ATA 게이트웨이에서 ATA 콘솔 바로 가기를 만드는 데 사용되는 ATA 콘솔의 IP 주소를 변경하는 방법에 대해 설명합니다."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 08/24/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: b3d11a87f1909c1fd964fa990e5d36a91691a844


---

*적용 대상: Advanced Threat Analytics 버전 1.7*



# ATA 구성 변경 - ATA 콘솔 URL

>[!div class="step-by-step"]
[« ATA 센터 인증서](modifying-ata-config-centercert.md)
[도메인 연결 암호 »](modifying-ata-config-dcpassword.md)

## ATA 콘솔 URL 변경
기본적으로 ATA 콘솔 URL은 ATA 센터를 설치할 때 ATA 콘솔 IP 주소에 대해 선택한 IP 주소입니다.

이 URL은 다음 시나리오에서 사용됩니다.

-   ATA 게이트웨이 설치 – ATA 게이트웨이가 설치되면 ATA 센터에 자동으로 등록됩니다. 이 등록 프로세스는 ATA 콘솔에 연결하면 수행됩니다. ATA 콘솔 URL에 대한 FQDN을 입력하면 ATA 게이트웨이가 ATA 콘솔이 바인딩되어 있는 IP 주소에 대한 FQDN을 확인할 수 있는지 검토해야 합니다.

-   경고 - ATA는 SIEM 또는 전자 메일 경고를 보낼 때 의심스러운 활동에 대한 링크를 포함합니다. 링크의 호스트 부분은 ATA 콘솔 URL 설정입니다.

-   내부 CA(인증 기관)에서 인증서를 설치한 경우 사용자가 ATA 콘솔에 연결할 때 경고 메시지가 표시되지 않도록 해당 URL을 인증서의 주체 이름과 일치하도록 만들 수 있습니다.

-   ATA 콘솔 URL에 대한 FQDN을 사용하면 이전에 전송된 경고를 중단하거나 ATA 게이트웨이 패키지를 다시 다운로드할 필요 없이, ATA 콘솔에서 사용되는 IP 주소를 수정할 수 있습니다. 새 IP 주소로 DNS를 업데이트하기만 하면 됩니다.

> [!NOTE]
> ATA 콘솔 URL을 수정한 후 새 데이터 게이트웨이 설치하기 전에 ATA 게이트웨이 설치 패키지를 다운로드해야 합니다.

ATA 콘솔에 대한 URL을 수정해야 하는 경우 ATA 센터 서버에서 다음 단계를 수행합니다.

1.  ATA 콘솔을 엽니다.

2.  도구 모음에서 설정 옵션을 선택하고 **구성**을 선택합니다.

    ![ATA 구성 설정 아이콘](media/ATA-config-icon.JPG)

3.  **Center**(센터)를 클릭합니다.

4.  **Console IP Address**(콘솔 IP 주소)에서 기존 IP 주소 중 하나를 선택합니다.

5.  필요에 따라 **콘솔 URL**에서 URL을 수정합니다.

    ![ATA 콘솔 URL](media/ATA-chge-center-URL.png)
6.  **저장**을 클릭합니다.

>[!div class="step-by-step"]
[« ATA 센터 인증서](modifying-ata-config-centercert.md)
[도메인 연결 암호 »](modifying-ata-config-dcpassword.md)


## 참고 항목
- [ATA 콘솔 작업](working-with-ata-console.md)
- [ATA 설치](install-ata.md)
- [ATA 포럼을 확인해 보세요!](https://aka.ms/ata-forum)



<!--HONumber=Aug16_HO5-->


