---
title: "Advanced Threat Analytics ATA 센터 구성 변경 | Microsoft Docs"
description: "ATA 센터의 IP 주소, 포트, 콘솔 URL 또는 인증서를 변경하는 방법을 설명합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4fe4569cd6477775e8a888d2acd05511f16fb5f6
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*



# <a name="modifying-the-ata-center-configuration"></a>ATA 센터 구성 수정


초기 배포 후 ATA 센터를 수정할 때는 신중하게 해야 합니다. 콘솔 URL 및 인증서를 업데이트할 때는 다음 절차를 사용합니다.

## <a name="the-ata-console-url"></a>ATA 콘솔 URL

이 URL은 다음 시나리오에서 사용됩니다.

-   ATA 게이트웨이에서 ATA 센터와 통신하는 데 사용하는 URL입니다.

- ATA 게이트웨이 설치 – ATA 게이트웨이가 설치되면 ATA 센터에 자동으로 등록됩니다. 이 등록 프로세스는 ATA 콘솔에 연결하면 수행됩니다. ATA 콘솔 URL의 FQDN을 입력할 때 ATA 게이트웨이에서 ATA 콘솔에 바인딩된 IP 주소에 대한 FQDN을 확인할 수 있어야 합니다.

-   경고 - ATA는 SIEM 또는 전자 메일 경고를 보낼 때 의심스러운 활동에 대한 링크를 포함합니다. 링크의 호스트 부분은 ATA 콘솔 URL 설정입니다.

-   내부 CA(인증 기관)에서 인증서를 설치한 경우 URL을 인증서의 주체 이름과 일치하게 만드세요. 그러면 사용자가 ATA 콘솔에 연결해도 경고 메시지를 받지 않게 됩니다.

-   ATA 콘솔 URL의 FQDN을 사용하면 이전 경고를 중단하거나 ATA 게이트웨이 패키지를 다시 다운로드할 필요 없이, ATA 콘솔에서 사용되는 IP 주소를 수정할 수 있습니다. 새 IP 주소로 DNS를 업데이트하기만 하면 됩니다.

1. 사용할 새 URL이 ATA 콘솔의 IP 주소인지 확인해야 합니다.

2. ATA 설정에서 **센터** 아래에 새 URL을 입력합니다. 이때 ATA 센터 서비스는 여전히 원래 URL을 사용합니다. 

 ![ATA 구성 변경](media/change-center-config.png)

  > [!NOTE]
  > 사용자 지정 IP 주소를 입력한 경우 해당 IP 주소를 ATA 센터에 설치할 때까지 **활성화**를 클릭할 수 없습니다.
    
3. ATA 게이트웨이가 동기화될 때까지 기다립니다. 이제 ATA 콘솔에 액세스할 수 있는 두 개의 잠재적인 URL이 있습니다. ATA 게이트웨이는 원래 URL을 사용하여 연결할 수 있는 한 새 URL을 사용하려고 시도하지 않습니다.

4. 모든 ATA 게이트웨이가 업데이트된 구성과 동기화된 후, 새 URL을 활성화합니다. 새 URL을 활성화하면 ATA 게이트웨이가 이제 새 URL을 사용하여 ATA 센터에 액세스합니다. ATA 게이트웨이는 ATA 센터 서비스에 연결된 후에 최신 구성을 끌어오고 ATA 콘솔의 새 URL만을 갖게 됩니다. 

> [!NOTE]
> -   새 URL을 활성화하는 동안 ATA 게이트웨이가 오프라인 상태여서 업데이트된 구성을 받지 못하면 구성 JSON 파일을 ATA 게이트웨이에서 수동으로 업데이트하세요.
> -   새 URL을 활성화한 후 새 데이터 게이트웨이 배포해야 하는 경우 ATA 게이트웨이 설치 패키지를 다시 다운로드해야 합니다.


## <a name="the-ata-center-certificate"></a>ATA 센터 인증서

> [!WARNING]
> - 기존 인증서의 갱신 프로세스가 지원되지 않습니다. 인증서를 갱신하는 방법은 새 인증서를 만들고 해당 인증서를 사용하도록 ATA를 구성하는 방법만이 유일합니다.


이 프로세스를 수행하여 인증서를 바꿉니다.

1. 현재 인증서가 만료되기 전에 새 인증서를 만들고 해당 인증서가 ATA 센터 서버에 설치되었는지 확인해야 합니다. <br></br>내부 인증 기관에서 인증서를 선택하는 것이 좋지만 새 자체 서명 인증서를 만들 수도 있습니다. 자세한 내용은 [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate)를 참조하세요.

2. ATA 설정의 **센터** 아래에서 새로 만들어진 이 인증서를 선택합니다. 이때 ATA 센터 서비스는 여전히 원래 인증서에 바인딩되어 있습니다. 

 ![ATA 구성 변경](media/change-center-config.png)

3. ATA 게이트웨이가 동기화될 때까지 기다립니다. 이제 상호 인증에 유효한 두 가지 잠재적인 인증서가 있습니다. ATA 게이트웨이는 원래 인증서를 사용하여 연결할 수 있는 한 새 인증서를 사용하려고 시도하지 않습니다.

4. 모든 ATA 게이트웨이가 업데이트된 구성과 동기화된 후에는 ATA 센터 서비스가 바인딩된 새 인증서를 활성화하세요. 새 인증서를 활성화하면 ATA 센터 서비스가 해당 인증서에 바인딩됩니다. 이제 ATA 게이트웨이가 새 인증서를 사용하여 ATA 센터를 인증합니다. ATA 게이트웨이는 ATA 센터 서비스에 연결한 후에 최신 구성을 끌어오고 ATA 센터에 대해 해당 새 인증서만을 갖게 됩니다. 

> [!NOTE]
> -   새 인증서를 활성화하는 동안 ATA 게이트웨이가 오프라인 상태여서 업데이트된 구성을 받지 못하면 구성 JSON 파일을 ATA 게이트웨이에서 수동으로 업데이트하세요.
> -   ATA 게이트웨이에서 신뢰하는 인증서를 사용해야 합니다.
> -   인증서는 또한 ATA 콘솔에서도 사용되므로 브라우저 경고 방지를 위해 ATA 콘솔 주소가 일치해야 합니다.
> -   새 인증서를 활성화한 후 새 데이터 게이트웨이 배포해야 하는 경우 ATA 게이트웨이 설치 패키지를 다시 다운로드해야 합니다.



 
## <a name="see-also"></a>참고 항목
- [ATA 콘솔 작업](working-with-ata-console.md)
- [ATA 포럼을 확인해 보세요!](https://aka.ms/ata-forum)
