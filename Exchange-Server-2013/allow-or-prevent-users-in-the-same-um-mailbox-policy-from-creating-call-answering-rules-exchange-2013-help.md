﻿---
title: 'Разрешить или запретить пользователям в одной политики почтовых ящиков единой системы обмена СООБЩЕНИЯМИ создавать правила ответа на звонок: Exchange 2013 Help'
TOCTitle: Разрешить или запретить пользователям в одной политики почтовых ящиков единой системы обмена СООБЩЕНИЯМИ создавать правила ответа на звонок
ms:assetid: e44acaa6-d5a8-41e8-94aa-100be0bd6391
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd351209(v=EXCHG.150)
ms:contentKeyID: 50556496
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Разрешить или запретить пользователям в одной политики почтовых ящиков единой системы обмена СООБЩЕНИЯМИ создавать правила ответа на звонок

 

_**Применимо к:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:**2013-02-22_

Можно разрешить пользователям, связанных с политикой почтовых ящиков единой системы обмена сообщениями (UM) для настройки правила ответа на звонок или запретить таким образом. Если параметр, чтобы настроить правила ответа на вызовы отключен на абонентской группы единой системы обмена СООБЩЕНИЯМИ, функцию правила ответа на звонок не будут доступны для пользователей с поддержкой единой системы обмена СООБЩЕНИЯМИ, связанные с политикой почтовых ящиков единой системы обмена СООБЩЕНИЯМИ. По умолчанию включен.

Дополнительные задачи управления, связанные с предоставлением пользователям разрешений на переадресацию вызовов, см. в разделе [Переадресация звонков процедур](forwarding-calls-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: 2 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Политики почтовых ящиков единой системы обмена сообщениями» в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что политика почтовых ящиков единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание политики почтовых ящиков единой системы обмена сообщениями](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="Совет" alt="Совет" />Совет.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Что необходимо сделать?

## Использование Центра администрирования Exchange для включения или отключения правил автоответчика в политике почтовых ящиков единой системы обмена сообщениями

1.  В Центре администрирования Exchange последовательно выберите пункты **Единая система обмена сообщениями** \> **Абонентские группы единой системы обмена сообщениями**. Выберите из списка абонентскую группу единой системы обмена сообщениями, которую необходимо изменить, и нажмите кнопку **Правка**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

2.  В разделе **Политики почтовых ящиков единой системы обмена сообщениями** выберите политику почтовых ящиков единой системы обмена сообщениями, которую требуется изменить, а затем нажмите кнопку **Изменить**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  На странице **Политика почтовых ящиков единой системы обмена сообщениями** установите или снимите флажок **Разрешить пользователям настраивать правила автоответчика**.

4.  Нажмите кнопку **Сохранить**.

## Использование командной консоли для включения или отключения правил ответа на вызовы для политики почтовых ящиков единой системы обмена сообщениями

В этом примере показано, как разрешить пользователям, связанным с политикой почтовых ящиков единой системы обмена сообщениями `MyUMMailboxPolicy`, создавать правила автоответчика.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $true

В этом примере пользователям, связанным с политикой почтовых ящиков единой системы обмена сообщениями `MyUMMailboxPolicy`, запрещается создавать правила ответа на вызовы.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $false
