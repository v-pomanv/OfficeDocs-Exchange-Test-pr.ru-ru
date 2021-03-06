﻿---
title: 'Создание списка адресов: Exchange 2013 Help'
TOCTitle: Создание списка адресов
ms:assetid: e86ba1b7-c41c-4050-bc29-13996cf53c59
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb125036(v=EXCHG.150)
ms:contentKeyID: 50489398
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewAddressListWizardForm.AddressListIntroductionPage
ms.translationtype: MT
---

# Создание списка адресов

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2012-10-12_

Списки адресов являются совокупностью получателей и других объектов Active Directory. Каждый список адресов содержит один или несколько типов объектов (например, пользователи, контакты, группы, общие папки, конференции и другие ресурсы). Списки адресов также позволяют разделять объекты с включенной поддержкой почты в Active Directory для определенных групп пользователей.

Дополнительные сведения о задачах управления, связанных со списками адресов, см. в статье [Процедуры списка адресов](address-list-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы?

  - Предполагаемое время для завершения: 5 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Списки адресов" в разделе [Разрешения для электронных адресов и адресных книг](email-address-and-address-book-permissions-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Что необходимо сделать?

## Использование центра управления Exchange для создания списка адресов

1.  Перейдите на вкладку **Организация** \> **Списки адресов**, и нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

2.  В разделе **Список адресов** введите имя и укажите типы получателей для включения в список.

3.  По умолчанию Exchange создает списки адресов, содержащие всех членов вашей организации. Чтобы создать уникальный пользовательский список адресов, нажмите кнопку **Добавить правило**.
    
    > [!IMPORTANT]  
    > Если правило не будет добавлено, будет создан список адресов, дублирующий один из списков адресов по умолчанию.


4.  В списке выберите параметр фильтрации (например, **Настраиваемый атрибут 1**).

5.  В поле **Укажите слова или фразы** введите слова или фразы для фильтра, нажмите **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления") и нажмите **ОК**.
    
    Вы можете добавить несколько фраз или слов, повторив шаг 4. Фильтр является логическим оператором **ИЛИ**. Например, можно создать фильтр, который будет применять список адресов к пользователям, у которых Настраиваемый атрибут 1 — **Орегон**, **Айдахо** или **Вашингтон**.

6.  (Необязательно) Нажмите кнопку **Добавить правило** еще раз, чтобы добавить фильтры. Дополнительные фильтры создают логический оператор **И**. Чем больше фильтров будет добавлено, тем меньшее количество пользователей появится в списке адресов.

7.  Нажмите кнопку **Предварительный просмотр получателей в списке адресов**, чтобы просмотреть получателей, к которым будет применяться этот список адресов.

8.  Нажмите кнопку **Сохранить**.

9.  Вы получите предупреждение, что список адресов не будет применяться, пока вы не обновите его. В зависимости от размера организации и фильтров, добавленных в список адресов, некоторые списки адресов могут содержать тысячи или десятки тысяч получателей. Обновление списков адресов может повлиять на ресурсы, поэтому желательно обновлять список в непиковые часы.
    
    Дополнительные сведения об обновлении списка адресов см. в статье [Обновление списка адресов](update-an-address-list-exchange-2013-help.md).

## Использование командной консоли для создания списка адресов

В этом примере создается список адресов MyAddressList с использованием параметра *RecipientFilter*, а также включаются получатели, являющиеся пользователями почтовых ящиков, у которых для параметра `StateOrProvince` заданы значения `Washington` или `Oregon`:

    New-AddressList -Name MyAddressList -RecipientFilter {((RecipientType -eq 'UserMailbox') -and ((StateOrProvince -eq 'Washington') -or (StateOrProvince -eq 'Oregon')))}

В этом примере создается дочерний список адресов «Building 34 Meeting Rooms» в родительском контейнере «All Rooms» с использованием встроенных условий.

    New-AddressList -Name "Building 34 Meeting Rooms" -Container "\All Rooms" -IncludedRecipients Resources -ConditionalCustomAttribute1 "Building 34"

Подробные сведения о синтаксисе и параметрах см. в разделе [New-AddressList](https://technet.microsoft.com/ru-ru/library/aa996912\(v=exchg.150\)).

