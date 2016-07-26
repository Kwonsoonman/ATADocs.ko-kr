---
title: "ATA 구성 변경 - ATA 콘솔 IP 주소 | Microsoft ATA"
description: "ATA 게이트웨이에서 ATA 콘솔 바로 가기를 만드는 데 사용되는 ATA 콘솔의 IP 주소를 변경하는 방법에 대해 설명합니다."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 3c02459e6a0cde359e632bf966948cf3a72170a2


---

# ATA 구성 변경 - ATA 콘솔 IP 주소

>[!div class="step-by-step"]
[« ATA 센터 인증서](modifying-ata-config-centercert.md)
[IIS 인증서 »](modifying-ata-config-iiscert.md)

## ATA 콘솔 IP 주소 변경
기본적으로 ATA 콘솔 URL은 ATA 센터를 설치할 때 ATA 콘솔 IP 주소에 대해 선택한 IP 주소입니다.

이 URL은 다음 시나리오에서 사용됩니다.

-   ATA 게이트웨이 설치 – ATA 게이트웨이가 설치되면 ATA 센터에 자동으로 등록됩니다. 이 등록 프로세스는 ATA 콘솔에 연결하면 수행됩니다. ATA 콘솔 URL에 대한 FQDN을 입력하면 ATA 게이트웨이가 ATA 콘솔이 바인딩되어 있는 IP 주소에 대한 FQDN을 IIS에서 확인할 수 있는지 검토해야 합니다. 또한 이 URL은 ATA 게이트웨이에 ATA 콘솔에 대한 바로 가기를 만드는 데 사용됩니다.

-   경고 - ATA는 SIEM 또는 전자 메일 경고를 보낼 때 의심스러운 활동에 대한 링크를 포함합니다. 링크의 호스트 부분은 ATA 콘솔 URL 설정입니다.

-   내부 CA(인증 기관)에서 인증서를 설치한 경우 사용자가 ATA 콘솔에 연결할 때 경고 메시지가 표시되지 않도록 해당 URL을 인증서의 주체 이름과 일치하도록 만들 수 있습니다.

-   ATA 콘솔 URL에 대한 FQDN을 사용하면 이전에 전송된 경고를 중단하거나 ATA 게이트웨이 패키지를 다시 다운로드할 필요 없이, ATA 콘솔에 대해 IIS에서 사용되는 IP 주소를 수정할 수 있습니다. 새 IP 주소로 DNS를 업데이트하기만 하면 됩니다.

> [!NOTE]
> ATA 콘솔 URL을 수정한 후 새 데이터 게이트웨이 설치하기 전에 ATA 게이트웨이 설치 패키지를 다운로드해야 합니다.

ATA 콘솔에 대해 IIS에서 사용되는 IP 주소를 수정해야 하는 경우 ATA 센터 서버에서 다음 단계를 수행합니다.

1.  ATA 센터 서버에서 IP 주소를 설치합니다.

2.  IIS(인터넷 정보 서비스) 관리자를 엽니다.

3.  서버 이름을 확장하고 **사이트**를 확장합니다.

4.  Microsoft ATA 콘솔 사이트를 선택하고 **작업** 창에서 **바인딩**을 클릭합니다.

    ![ATA 콘솔 바인딩 작업 이미지](media/ATA-console-change-IP-bindings.jpg)

5.  **HTTP**를 선택하고 **편집**을 클릭하여 새 IP 주소를 선택합니다. **HTTPS**에 대해서도 동일한 IP 주소를 선택하여 동일하게 작업합니다.

    ![사이트 바인딩 편집 이미지](media/ATA-change-console-IP.jpg)

6.  **작업** 창의 **웹 사이트 관리**에서 **다시 시작**을 클릭합니다.

7.  관리자 명령 프롬프트를 열고 다음 명령을 입력하여 HTTP.SYS 드라이버를 업데이트합니다.

    -   새 IP 주소 추가 - `netsh http add iplisten ipaddress=newipaddress`

    -   새 주소가 사용되는지 확인 -  `netsh http show iplisten`

    -   이전 IP 주소 삭제 -  `netsh http delete iplisten ipaddress=oldipaddress`

8.  ATA 콘솔 URL이 여전히 IP 주소를 사용하고 있는 경우 ATA 콘솔 URL을 새 IP 주소로 업데이트하고 새 ATA 게이트웨이를 배포하기 전에 ATA 게이트웨이 설치 패키지를 다운로드합니다.

9. ATA 콘솔 URL이 FQDN인 경우 DNS를 해당 FQDN에 대한 새 IP 주소로 업데이트합니다.

>[!div class="step-by-step"]
[« ATA 센터 인증서](modifying-ata-config-centercert.md)
[IIS 인증서 »](modifying-ata-config-iiscert.md)


## 참고 항목
- [ATA 콘솔 작업](working-with-ata-console.md)
- [ATA 설치](install-ata.md)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


