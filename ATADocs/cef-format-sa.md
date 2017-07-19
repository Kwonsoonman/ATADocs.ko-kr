---
title: "ATA SIEM 로그 참조 | Microsoft Docs"
description: "ATA에서 SIEM으로 전송된 의심스러운 활동 로그의 샘플을 제공합니다."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/21/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: ca460647fbed07820e8d19083d5aca19a05bc0a8
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/30/2017
---
*적용 대상: Advanced Threat Analytics 버전 1.8*


# <a name="ata-siem-log-reference"></a>ATA SIEM 로그 참조

ATA는 의심스러운 활동 및 모니터링 경고 이벤트를 SIEM에 전달할 수 있습니다. 의심스러운 활동 이벤트는 CEF 형식입니다. 이 참조 문서에서는 SIEM에 전송된 의심스러운 활동 로그의 샘플을 제공합니다.

## <a name="sample-ata-suspicious-activities-in-cef-format"></a>CEF 형식의 ATA 의심스러운 활동 샘플
다음 필드 및 해당 값이 SIEM에 전달됩니다.

-   start – 경고의 시작 시간
-   suser – 이 경고와 관련된 계정(일반적으로 사용자 계정이어야 함)
-   shost – 이 경고에 대한 원본 컴퓨터
-   outcome – 해당 경고에서 수행된 활동의 성공/실패가 있다는 경고 결과  
-   msg – 경고에 대한 설명
-   cnt – 경고가 발생한 횟수가 있는 경고 카운트(예: 상당한 개수의 추측된 암호가 있는 무차별 암호 대입(brute force))
-   app – 이 경고에 사용된 프로토콜
-   externalId – ATA가 이 경고에 해당하는 이벤트 로그에 쓰는 이벤트 ID
-   cs#label & cs# – CEF가 사용하도록 허용하는 고객 문자열. cs#label은 새 필드의 이름이고, cs#은 값입니다(예: cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa).

이 예제에서 cs1은 경고에 대한 URL이 있는 필드입니다.

## <a name="sample-logs"></a>샘플 로그

우선 순위: 3=낮음 5=보통 10=높음

### <a name="bruteforce--ldap"></a>BruteForce – LDAP
05-03-2017          13:35:01               Auth.Warning    192.168.0.220     May  3 10:35:01 CENTER ATA:CEF:0|Microsoft|ATA|.5942.64854|BruteForceSuspiciousActivity|LDAP 단순 바인딩을 사용한 무차별 암호 대입 공격(brute force attack)|5|start=2017-05-03T10:34:57.2785534Z app=Ldap suser=Darris Woods shost=CLIENT1 msg=CLIENT1에서 Darris Woods(소프트웨어 엔지니어)에 대해 LDAP 프로토콜을 사용한 무차별 암호 대입 공격(brute force attack)이 시도되었습니다(76회 추측 시도). cnt=76 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     May  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|LDAP 단순 바인딩을 사용한 무차별 암호 대입 공격(brute force attack)|5|start=2017-05-03T10:34:58.7004159Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=CLIENT1에서 Dino Hopkins(소프트웨어 엔지니어)에 대해 LDAP 프로토콜을 사용한 무차별 암호 대입 공격(brute force attack)이 시도되었습니다(3회 추측 시도). cnt=3 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     May  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|LDAP 단순 바인딩을 사용한 무차별 암호 대입 공격(brute force attack)|5|start=2017-05-03T10:34:59.7269332Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=CLIENT1에서 Dino Hopkins(소프트웨어 엔지니어)에 대해 LDAP 프로토콜을 사용한 성공적인 무차별 암호 대입 공격(brute force attack)이 시도되었습니다(77회 추측 시도). cnt=77 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70
### <a name="bruteforce"></a>BruteForce
05-14-2017          13:27:05               Auth.Warning    192.168.0.220     1 2017-05- ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|BruteForceSuspiciousActivity|의심스러운 인증 실패|5|start=2017-05-14T10:27:04.3904739Z app=Kerberos shost=CLIENT1 msg=CLIENT1에서 잠재적 무차별 암호 대입 공격(brute force attack)을 나타내는 의심스러운 인증 실패가 검색되었습니다. externalId=2023 cs1Label=url cs1=https://center/suspiciousActivity/591830f98ca1ec11d0c0d7f5
### <a name="privilege-escalation"></a>권한 상승
#### <a name="silver"></a>실버
05-10-2017          17:14:15               Auth.Error           192.168.0.220     1 2017-05-10T14:14:15.589415+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|위조된 권한 부여 데이터를 사용한 권한 상승|10|start=2017-05-10T14:11:51.8053059Z app=Kerberos suser=user1 msg=user1이 CLIENT2에서 위조된 권한 부여 데이터를 사용하여 권한을 HOST/client1로 상승하려고 시도했습니다. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/591320378ca1ec02543e4747
#### <a name="gold"></a>Gold
05-10-2017          17:13:30               Auth.Error           192.168.0.220     1 2017-05-10T14:13:30.244377+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|위조된 권한 부여 데이터를 사용한 권한 상승|10|start=2017-05-10T14:11:27.6455273Z app=Kerberos suser=user1 msg=user1이 CLIENT1에서 위조된 권한 부여 데이터를 사용하여 DC4에 대해 권한 상승을 시도했습니다. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/5913200a8ca1ec02543e3ea8
### <a name="golden-ticket"></a>골든 티켓
05-14-2017          15:57:10               Auth.Warning    192.168.0.220     1 2017-05-14T12:57:10.392730+00:00 CENTER ATA 4732 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|암호화 다운그레이드 활동|5|start=2017-05-14T12:55:08.6913033Z app=Kerberos msg=CLIENT1에서 보낸 TGS_REQ 메시지의 TGT 필드에 대한 암호화 방법이 이전에 학습된 행동에 따라 다운그레이드되었습니다. 이는 CLIENT1에서 사용 중인 골든 티켓의 결과일 수 있습니다. externalId=2009 cs1Label=url cs1=https://center/suspiciousActivity/591854268ca1ec127ceec396
### <a name="honey-token-activity"></a>Honey Token 활동
05-11-2017          16:49:10               Auth.Warning    192.168.0.220     1 2017-05-11T13:49:10.725605+00:00 CENTER ATA 876 HoneytokenActivitySuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|HoneytokenActivitySuspiciousActivity|Honeytoken 활동|5|start=2017-05-11T13:49:09.6455794Z app=Kerberos suser=privtriservice msg=privtriservice에서 다음 활동을 수행했습니다.\r\nDC1을 통한 회사 리소스에 대해 DC1에서 NTLM을 사용하여 인증했습니다. externalId=2014 cs1Label=url cs1=https://center/suspiciousActivity/59146bd68ca1ec036ce57d29
### <a name="suspicious-replication-of-directory-services"></a>디렉터리 서비스의 의심스러운 복제
May  3 11:02:28 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DirectoryServicesReplicationSuspiciousActivity|디렉터리 서비스의 악의적인 복제|10|start=2017-05-03T11:00:13.6560919Z suser=user1 shost=CLIENT1 outcome=Failure msg=CLIENT1에서 user1이 DC1에 대해 악의적인 복제 요청을 시도했습니다. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b8c48ca1ec04d05ed28d
### <a name="malicious-data-protection-private-information-request"></a>악성 데이터 보호 개인 정보 요청
May  3 13:39:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RetrieveDataProtectionBackupKeySuspiciousActivity|악의적인 데이터 복제 개인 정보 요청|10|start=2017-05-03T13:37:06.4039886Z app=LsaRpc shost=CLIENT1 suser= outcome=Success msg=CLIENT1에서 알 수 없는 사용자가 DC1에서 DPAPI 도메인 백업 키를 검색하려고 4회 시도했으며 성공했습니다. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dd868ca1ec04d05fb01d
### <a name="massive-object-deletion"></a>대규모 개체 삭제
05-14-2017          14:38:34               Auth.Warning    192.168.0.220     1 2017-05-14T11:38:34.898810+00:00 CENTER ATA 3748 MassiveObjectDeletionSuspiciousA ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|MassiveObjectDeletionSuspiciousActivity|대규모 개체 삭제|5|start=2017-05-14T11:33:32.0000000Z msg=시간이 지정되지 않은 기간 동안 496개 개체(총 AD 개체 중 9.75%)가 domain1.test.local 도메인에서 삭제되었습니다 cnt=496 externalId=2016 cs1Label=url cs1=https://center/suspiciousActivity/591841ba8ca1ec0ea4ad587a
### <a name="over-pass-the-hash"></a>Over-Pass-the-Hash
05-14-2017          12:07:46               Auth.Warning    192.168.0.220     1 2017-05-14T09:07:46.652319+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|암호화 다운그레이드 활동|5|start=2017-05-14T09:07:44.9933773Z app=Kerberos msg=CLIENT1에서 보낸 AS_REQ 메시지의 Encrypted_Timestamp 필드에 대한 암호화 방법이 이전에 학습된 행동에 따라 다운그레이드되었습니다. 이는 CLIENT1에서 Over-Pass-the-Hash를 사용한 인증서 도용을 수행한 결과일 수 있습니다. externalId=2010 cs1Label=url cs1=https://center/suspiciousActivity/59181e628ca1ec045cdfa929
### <a name="pass-the-hash"></a>Pass-the-Hash
05-10-2017          17:48:51               Auth.Error           192.168.0.220     1 2017-05-10T14:48:51.998620+00:00 CENTER ATA 596 PassTheHashSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|PassTheHashSuspiciousActivity|Pass-the-Hash 공격을 사용한 ID 도용|10|start=2017-05-10T14:46:50.9463800Z app=Ntlm suser=user2 msg=user2가 이전에 CLIENT1에서 로그인하여 사용한 컴퓨터 중 하나에서 user2의 해시가 도난당했습니다. externalId=2017 cs1Label=url cs1=https://center/suspiciousActivity/591328538ca1ec02543f9a1a
### <a name="account-enumeration"></a>계정 열거
05-10-2017          16:44:22               Auth.Warning    192.168.0.220     1 2017-05-10T13:44:22.706381+00:00 CENTER ATA 596 AccountEnumerationSuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|AccountEnumerationSuspiciousActivity|계정 열거를 사용한 정찰|5|start=2017-05-10T13:44:20.9930644Z app=Kerberos shost=CLIENT3 msg=CLIENT3에서 시작된, Kerberos 프로토콜을 사용한 의심스러운 계정 열거 활동이 검색되었습니다. 공격자가 계정 이름에 대해 총 72회 추측 시도를 수행했으며, 2회의 추측 시도가 Active Directory의 기존 계정 이름과 일치했습니다. externalId=2003 cs1Label=url cs1=https://center/suspiciousActivity/591319368ca1ec02543c56ee
### <a name="dns-recon"></a>DNS 정찰
05-03-2017          13:16:57               Auth.Warning    192.168.0.220     May  3 10:16:57 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|DNS를 사용한 정찰|5|start=2017-05-03T10:16:41.8297467Z app=Dns shost=CLIENT1 msg=CLIENT1(DNS 서버 아님)에서 DC1에 대해 시작된 의심스러운 DNS 활동이 관찰되었습니다. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa 05-03-2017          13:24:21               Auth.Warning    192.168.0.220     May  3 10:24:21 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|DNS를 사용한 정찰|5|start=2017-05-03T10:24:08.0950753Z app=Dns shost=CLIENT1 request=contoso.com requestMethod=Axfr reason=NameError outcome=Failure msg=CLIENT1(DNS 서버 아님)에서 시작된 의심스러운 DNS 활동이 관찰되었습니다. contoso.com에 대해 쿼리가 수행되었습니다(유형 Axfr). 응답은 NameError였습니다. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
### <a name="smb-session-enumeration"></a>SMB 세션 열거
May  3 11:55:43 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|EnumerateSessionsSuspiciousActivity|SMB 세션 열거를 사용한 정찰|5|start=2017-05-03T11:52:02.4360718Z app=SrvSvc shost=CLIENT1 msg=CLIENT1에서 DC1에 대해 SMB 세션 열거 시도가 성공적으로 수행되었으며 user1(daf::1)이 공개되었습니다. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c53f8ca1ec04d05f1cf1
### <a name="samr-enumeration"></a>SAMR 열거
May  3 11:44:48 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|SamrReconnaissanceSuspiciousActivity|디렉터리 서비스 열거를 사용한 정찰|5|start=2017-05-03T11:42:46.5911225Z app=Samr shost=CLIENT1 suser=user1 outcome=Success msg=CLIENT1에서 DC1에 대해 SAMR 프로토콜을 사용한 다음 디렉터리 서비스 열거가 수행되었습니다.\r\nuser1이 domain1.test.local에 있는 모든 그룹을 성공적으로 열거했습니다. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c2b08ca1ec04d05f0e19
### <a name="remote-execution"></a>원격 실행
May  3 12:36:47 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RemoteExecutionSuspiciousActivity|원격 실행 시도 검색됨|3|start=2017-05-03T12:34:32.3714348Z app=ServiceControl shost=CLIENT1 suser=Administrator outcome=CLIENT1에서 DC1에 대해 다음 원격 실행 시도가 수행되었습니다.\r\n관리자가 PSEXESVC를 원격으로 만드는 데 성공했습니다. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cedf8ca1ec04d05f5692
### <a name="skeleton-key"></a>스켈레톤 키
05-14-2017          12:13:12               Auth.Warning    192.168.0.220     1 2017-05-14T09:13:12.102468+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|암호화 다운그레이드 활동|5|start=2017-05-14T09:13:03.3509467Z app=Kerberos msg=CLIENT2에서 보낸 KRB_ERR 메시지의 ETYPE_INFO2 필드에 대한 암호화 방법이 이전에 학습된 행동에 따라 다운그레이드되었습니다. 이는 DC3에 있는 스켈레톤 키의 결과일 수 있습니다. externalId=2011 cs1Label=url cs1=https://center/suspiciousActivity/59181fa88ca1ec045cdfe630
### <a name="unusual-protocol-implementation"></a>비정상적인 프로토콜 구현
May  3 12:28:19 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|AbnormalProtocolSuspiciousActivity|비정상적인 프로토콜 구현|5|start=2017-05-03T12:28:05.3561302Z app=Ntlm shost=CLIENT1 suser=Administrator outcome=Success msg=관리자가 CLIENT1에서 비정상적인 프로토콜 구현을 사용하여 DC1에 대해 성공적으로 인증했습니다. 이는 Pass-the-Hash, 무차별 암호 대입(Brute force) 등의 공격을 실행하는 데 사용된 악성 도구의 결과일 수 있습니다. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4
### <a name="sensitive-account-credentials-exposed"></a>중요한 계정 자격 증명 공개됨
May  3 13:23:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|중요한 계정 자격 증명 공개됨|3|start=2017-05-03T13:23:09.7798589Z app=Ldap shost=CLIENT1 suser=Administrator msg=관리자 자격 증명이 CLIENT1에서 LDAP 단순 바인딩을 사용하여 일반 텍스트로 공개되었습니다. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909d9c68ca1ec04d05f9918
### <a name="services-exposing-account-credentials"></a>계정 자격 증명을 공개하는 서비스
May  3 13:34:23 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|계정 자격 증명을 공개하는 서비스|3|start=2017-05-03T13:28:36.5159194Z app=Ldap shost=daf::220 msg=daf::220(daf::220)에서 실행 중인 서비스가 LDAP 단순 바인딩을 사용하여 계정 자격 증명을 일반 텍스트로 공개합니다. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dc5f8ca1ec04d05fa8b1
### <a name="pass-the-ticket"></a>Pass-the-Ticket
May  4 13:15:41 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|PassTheTicketSuspiciousActivity|Pass-the-Ticket 공격을 사용한 ID 도용|10|start=2017-05-04T13:13:44.5160000Z app=Kerberos shost=CLIENT1 suser=Administrator request=krbtgt/DOMAIN1.TEST.LOCAL msg=관리자의 Kerberos 티켓이 CLIENT2에서 CLIENT1로 도난당했으며 krbtgt/DOMAIN1.TEST.LOCAL에 액세스하는 데 사용되었습니다. cs2Label=ticketSourceComputer cs2=CLIENT2 cs3Label=ticketSourceComputerIpAddress cs3= cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/590b29168ca1ec0ba438acf6

## <a name="see-also"></a>참고 항목
- [ATA 필수 구성 요소](ata-prerequisites.md)
- [ATA 용량 계획](ata-capacity-planning.md)
- [이벤트 수집 구성](configure-event-collection.md)
- [Windows 이벤트 전달 구성](configure-event-collection.md#configuring-windows-event-forwarding)
- [ATA 포럼을 확인해 보세요!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
