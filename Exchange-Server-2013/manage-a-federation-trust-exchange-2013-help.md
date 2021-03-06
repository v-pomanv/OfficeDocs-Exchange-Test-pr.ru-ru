﻿---
title: 'Управление доверием федерации: Exchange 2013 Help'
TOCTitle: Управление доверием федерации
ms:assetid: 0439839f-2052-4bc9-9d30-aa6e7d51b733
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ673036(v=EXCHG.150)
ms:contentKeyID: 50487369
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Управление доверием федерации

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2015-01-01_

Отношение доверия федерации создает связь доверия между организацией Microsoft Exchange 2013 и системой проверки подлинности Azure Active Directory, а также поддерживает федеративный общий доступ с другими федеративными организациями Exchange. Обычно не требуется контролировать или изменять доверие федерации после его создания. Однако могут быть ситуации, в которых необходимо добавить или удалить федеративные домены или сбросить домен, используемый для настройки идентификатора организации (OrgID) для доверия федерации.

> [!NOTE]  
> Изменение существующего доверия федерации, особенно основного общего домена, используемого для определения OrgID, может нарушить федеративный общий доступ между федеративными организациями Exchange или гибридными развертываниями с организациями Office 365.


Дополнительные сведения об управленческих задачах, связанных с федерацией, см. в разделе [Процедуры федерации](federation-procedures-exchange-2013-help.md).

> [!IMPORTANT]  
> Эта возможность Exchange Server 2013 не совместима полностью со службой Office 365, предоставляемой компанией 21Vianet в Китае. Кроме того, возможны некоторые ограничения. <a href="https://go.microsoft.com/fwlink/?linkid=313640">Дополнительные сведения о службе Office 365, предоставляемой компанией 21Vianet</a>.


## Что нужно знать перед началом работы?

  - Осталось времени до завершения: 30 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье *Federation and certificates* запись о разрешениях в разделе [Разрешения инфраструктуры Exchange и командной консоли](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - Вам потребуется добавить запись TXT в общедоступную систему DNS для каждого нового федеративного домена, добавленное в доверие федерации. Просмотрите требования по добавлению TXT-записи вместе с организацией, в которой размещены общедоступные DNS-записи.

  - В целях этого раздела существующее доверие федерации было настроено со следующими параметрами:
    
      - **Contoso.com** является основным общим доменом для доверия федерации. (Этот домен не изменятся.)
    
      - Федеративные домены **service.contoso.com** и **sales.contoso.com** включаются в существующее доверие федерации.
    
      - **Marketing.contoso.com** является обслуживаемым доменом в организации Exchange.

  - В этом разделе также описываются другие задачи управления федерацией, такие как просмотр сертификатов, используемых для доверия федерации, и управление ими, а также просмотр сведений о параметрах доверия федерации в командной консоли.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Что необходимо сделать?

## Использование центра администрирования Exchange для управления доверием федерации

1.  На сервере Exchange 2013 в локальной организации последовательно выберите пункты **Организация** \> **Общий доступ**.

2.  В разделе **Доверие федерации** нажмите кнопку **Изменить**.

3.  В окне **Общие домены** пропустите **Шаг 1**, так как основной общий домен не изменяется.

4.  В окне **Шаг 2** выберите домен **service.contoso.com** и нажмите кнопку **Удалить**![Значок "Удалить"](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Значок \"Удалить\""), чтобы удалить домен из доверия федерации.

5.  В разделе **Шаг 2** нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

6.  В окне **Выбор обслуживаемых доменов** выберите **marketing.contoso.com** из списка обслуживаемых доменов и нажмите кнопку **ОК**, чтобы добавить домен в доверие федерации.
    
    > [!IMPORTANT]  
    > Для домена <strong>marketing.contoso.com</strong> будет создана строка подтверждения федеративного домена. Вы должны создать отдельную запись TXT для этого домена в общедоступной системе DNS.


7.  С использованием строки подтверждения федеративного домена, созданной для домена **marketing.contoso.com**, создайте запись TXT на общедоступном сервере DNS. В зависимости от расписания обновления общедоступного узла DNS для репликации изменений DNS может понадобиться 15 минут или более.

8.  После того, как запись TXT создается и реплицируется, нажмите кнопку **Обновить**.

## Использование командной консоли Exchange для управления доверием федерации

1.  Этот пример удаляет домен service.contoso.com из доверия федерации.
    
        Remove-FederatedDomain -DomainName service.contoso.com

2.  В этом примере домен marketing.contoso.com добавляется к доверию федерации.
    
        Add-FederatedDomain -DomainName marketing.contoso.com

Дополнительные сведения о синтаксисе и параметрах см. в разделах [Remove-FederatedDomain](https://technet.microsoft.com/ru-ru/library/dd298128\(v=exchg.150\)) и [Add-FederatedDomain](https://technet.microsoft.com/ru-ru/library/dd351208\(v=exchg.150\)).

Выполните следующие команды консоли для управления другими аспектами доверия федерации:

1.  **Просмотр федеративных OrgID и федеративных доменов**
    
    Этот пример отображает федеративный OrgID организации Exchange и связанные сведения, в том числе федеративные домены и состояние.
    
        Get-FederatedOrganizationIdentifier

2.  **Просмотр сертификатов доверия федерации**
    
    В этом примере показаны предыдущий, текущий и следующий сертификаты, используемые доверием федерации "Проверка подлинности Azure AD".
    
        Get-FederationTrust "Azure AD authentication" | Select Org*certificate

3.  **Проверка состояния сертификатов федерации**
    
    В этом примере показано состояние сертификатов федерации на всех серверах почтовых ящиков и клиентского доступа в организации.
    
        Test-FederationTrustCertificate

4.  **Настройка доверия федерации для использования сертификата в качестве следующего сертификата**
    
    В этом примере настраивается использование доверием федерации "Проверка подлинности Azure AD" сертификата с отпечатком в качестве следующего сертификата. После развертывания сертификата на всех серверах Exchange в организации можно настроить использование этого сертификата в качестве текущего сертификата с помощью переключателя *PublishCertificate*.
    
        Set-FederationTrust "Azure AD authentication" -Thumbprint AC00F35CBA8359953F4126E0984B5CCAFA2F4F17

5.  **Настройка использования доверием федерации следующего сертификата в качестве текущего сертификата**
    
    В этом примере для доверия федерации "Проверка подлинности Azure AD" настраивается использование следующего сертификата в качестве текущего сертификата, который затем публикуется в системе проверки подлинности Azure AD.
    
        Set-FederationTrust "Azure AD authentication" -PublishFederationCertificate
    
    > [!CAUTION]  
    > Прежде чем настраивать для доверия федерации использование следующего сертификата в качестве текущего сертификата федерации, убедитесь, что этот сертификат развернут на всех серверах Exchange в организации. Используйте командлет <a href="https://technet.microsoft.com/ru-ru/library/dd335228(v=exchg.150)">Test-FederationTrustCertificate</a> для проверки состояния развертывания сертификата.


6.  **Обновление метаданных федерации и сертификата из системы проверки подлинности Azure AD**
    
    В этом примере обновляются метаданные федерации и сертификат из системы проверки подлинности Azure AD для доверия федерации "Проверка подлинности Azure AD".
    
        Set-FederationTrust "Azure AD authentication" -RefreshMetadata

Подробные сведения о синтаксисе и параметрах см. в следующих разделах:

  - [Get-FederatedOrganizationIdentifier](https://technet.microsoft.com/ru-ru/library/dd298149\(v=exchg.150\))

  - [Get-FederationTrust](https://technet.microsoft.com/ru-ru/library/dd351262\(v=exchg.150\))

  - [Test-FederationTrustCertificate](https://technet.microsoft.com/ru-ru/library/dd335228\(v=exchg.150\))

  - [Set-FederationTrust](https://technet.microsoft.com/ru-ru/library/dd298034\(v=exchg.150\))

## Как проверить, что все получилось?

Первым признаком правильной настройки доверия федерации будет успешное завершение мастера **общих доменов**.

Для дальнейшей проверки выполните следующее:

1.  Чтобы проверить сведения о доверии федерации, выполните следующую команду командной консоли Exchange.
    
        Get-FederationTrust | format-list

2.  Чтобы убедиться, что сведения о федерации можно извлечь из организации, выполните следующую команду командной консоли Exchange. Например, проверьте, возвращаются ли домены sales.contoso.com и marketing.contoso.com в параметре *DomainNames*.
    
        Get-FederationInformation -DomainName <your primary sharing domain>

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.

