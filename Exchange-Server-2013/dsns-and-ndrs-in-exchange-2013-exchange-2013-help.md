﻿---
title: 'Уведомления о доставке и отчеты о недоставке в Exchange 2013: Exchange 2013 Help'
TOCTitle: Уведомления о доставке и отчеты о недоставке в Exchange 2013
ms:assetid: 8e91de84-76fa-49b2-898c-c5eface76560
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb232118(v=EXCHG.150)
ms:contentKeyID: 50488595
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Уведомления о доставке и отчеты о недоставке в Exchange 2013

 

_**Применимо к:**Exchange Server 2013_

_**Последнее изменение раздела:**2016-12-09_

<table>
<thead>
<tr class="header">
<th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Справочную информацию об отчетах о недоставке в Office 365 или Exchange Online можно найти в статье <a href="https://go.microsoft.com/fwlink/p/?linkid=524931">Отчет о недоставке в Office 365</a>.</td>
</tr>
</tbody>
</table>


Если возникает проблема с доставкой сообщения, Exchange Server 2013 отсылает отправителю сообщение о недоставке. Оно содержит код ошибки, технические сведения о проблеме и иногда инструкции по ее устранению для отправителя сообщения. В этой статье, предназначенной для администраторов электронной почты, описаны возможные причины многих проблем с доставкой и способы их решения. Кроме того, вы узнаете, как правильно читать и интерпретировать отчеты о недоставке.

**Содержание**

Частые расширенные коды состояния

Разделы отчета о недоставке

Примеры

## Частые расширенные коды состояния

В следующей таблице приведены расширенные коды состояния, которые возвращаются в отчетах о недоставке в наиболее распространенных случаях сбоя доставки.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Расширенный код состояния</th>
<th>Описание</th>
<th>Возможная причина</th>
<th>Дополнительные сведения</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>4.3.1</p></td>
<td><p><code>Insufficient system resources</code></p></td>
<td><p>Произошла ошибка нехватки памяти. Причиной ошибки может быть проблема с ресурсом, например нехватка места на диске.</p>
<p>Вместо ошибки переполнения диска может возникать ошибка нехватки памяти.</p></td>
<td><p>Убедитесь, что на диске сервера Exchange достаточно свободного места.</p></td>
</tr>
<tr class="even">
<td><p>4.3.2</p></td>
<td><p><code>System not accepting network messages</code></p></td>
<td><p>Данный отчет о недоставке формируется при замораживании очереди.</p></td>
<td><p>Устранить проблему можно, разморозив очередь.</p></td>
</tr>
<tr class="odd">
<td><p>4.4.1</p></td>
<td><p><code>Connection timed out</code></p></td>
<td><p>Конечный сервер не отвечает. Эта ошибка может быть вызвана временными проблемами с сетью. Сервер Exchange автоматически пытается подключиться к серверу снова и доставить почту. Если после нескольких попыток почта не доставлена, создается отчет о недоставке с кодом неустранимой ошибки.</p></td>
<td><p>Следите за ситуацией. Возможно, это временная проблема, которая исчезнет сама собой.</p></td>
</tr>
<tr class="even">
<td><p>4.4.2</p></td>
<td><p><code>Connection dropped</code></p></td>
<td><p>Разрыв соединения между серверами. Эта ошибка может возникнуть из-за временных проблем с сетью или неполадок сервера. В течение заданного периода времени отправляющий сервер будет пытаться доставить сообщение, а затем будет создавать дальнейшие отчеты о состоянии.</p></td>
<td><p>Следите за ситуацией, пока сервер пытается доставить сообщение. Возможно, это временная проблема, которая исчезнет сама собой.</p>
<p>Данная ситуация может также возникнуть при достижении действующего для подключения ограничения размера сообщений или превышении заданного ограничения частоты отправки сообщений на IP-адрес клиента.</p></td>
</tr>
<tr class="odd">
<td><p>4.4.7</p></td>
<td><p><code>Message expired</code></p></td>
<td><p>Срок действия сообщения в очереди истек. Отправляющий сервер попытался ретранслировать или доставить сообщение, но операция не была завершена до истечения срока действия сообщения. Данное сообщение может также указывать на достижение ограничения заголовка сообщения на удаленном сервере или на истечение времени ожидания другого протокола при взаимодействии с удаленным сервером.</p></td>
<td><p>Данное сообщение обычно свидетельствует о проблеме на принимающем сервере. Проверьте допустимость адреса получателя и выясните, правильно ли настроен принимающий сервер для получения сообщений.</p>
<p>Возможно, следует уменьшить количество получателей в заголовке сообщения для узла, в связи с которым возникает ошибка. При повторной отправке этого сообщения оно снова будет помещено в очередь. Если принимающий сервер доступен, сообщение будет доставлено.</p></td>
</tr>
<tr class="even">
<td><p>5.0.0</p></td>
<td><p><code>HELO / EHLO requires domain address</code></p></td>
<td><p>Данная ситуация является постоянным сбоем. Некоторые ее причины описаны ниже.</p>
<ul>
<li><p>Нет маршрута для конкретного адресного пространства; например, SMTP-соединитель настроен, но адрес ему не соответствует.</p></li>
<li><p>Служба DNS возвратила доверенный сайте, не найденный в домене.</p></li>
<li><p>Произошла ошибка SMTP.</p></li>
</ul></td>
<td><p>Возможные способы решения проблемы указаны ниже.</p>
<ul>
<li><p>На одном или нескольких соединителях SMTP добавьте звездочку (<strong>*</strong>) в качестве адресного пространства SMTP.</p></li>
<li><p>Убедитесь, что служба DNS работает.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>5.1.0</p></td>
<td><p><code>Sender denied</code></p></td>
<td><p>Этот отчет о недоставке связан с общей ошибкой (неправильный адрес). Не удалось найти адрес электронной почты или другой атрибут в доменных службах Active Directory. Причиной проблемы могут быть записи контактов без атрибута <strong>targetAddress</strong>. Эта ошибка также может возникнуть, если не удалось определить атрибут <strong>homeMDB</strong> пользователя. Атрибут <strong>homeMDB</strong> соответствует серверу Exchange, на котором находится почтовый ящик пользователя.</p>
<p>Эта ошибка также может возникнуть, если вы сохранили сообщение электронной почты в виде файла с помощью Microsoft Outlook, а затем кто-то открыл его в автономном режиме и ответил на него. Свойство сообщения сохраняет атрибут <strong>legacyExchangeDN</strong>, только когда Outlook доставляет сообщение, поэтому поиск мог завершиться ошибкой.</p></td>
<td><p>Или адрес получателя отформатирован неправильно, или не удалось правильно выполнить разрешение получателя. При устранении этой ошибки прежде всего следует проверить адрес получателя и отправить сообщение повторно.</p></td>
</tr>
<tr class="even">
<td><p>5.1.1</p></td>
<td><p><code>Bad destination mailbox address</code></p></td>
<td><p>Возможные причины этой ошибки:</p>
<ul>
<li><p>Отправитель неправильно указал адрес электронной почты получателя.</p></li>
<li><p>Адрес получателя не существует в целевой системе электронной почты.</p></li>
<li><p>Почтовый ящик получателя перемещен, а кэш получателей Outlook на компьютере отправителя не обновлен.</p></li>
<li><p>Недопустимое устаревшее доменное имя почтового ящика получателя в доменной службе Active Directory.</p></li>
</ul></td>
<td><p>Эта ошибка обычно возникает в том случае, когда отправитель сообщения неправильно вводит адрес электронной почты получателя. Отправитель должен проверить адрес электронной почты получателя и повторить отправку. Эта ошибка может также возникать в том случае, если адрес электронной почты ранее был правильным, но изменился или был удален из конечной почтовой системы.</p>
<p>Если отправитель сообщения находится в той же организации Exchange, что и получатель, и почтовый ящик получателя все еще существует, определите, не перемещен ли он на новый почтовый сервер. Если это так, возможно, Outlook неправильно обновил кэш получателей. Попросите отправителя удалить адрес получателя из кэша получателей Outlook, а затем создать новое сообщение. При повторной отправке исходного сообщения возникнет та же ошибка.</p>
<p>Причиной этой ошибки могут быть другие проблемы, например недопустимое устаревшее различающееся имя в доменных службах Active Directory. Проверьте и исправьте устаревшее различающееся имя почтового ящика получателя. Затем попросите отправителя удалить адрес получателя из кэша получателей Outlook и создать новое сообщение. При повторной отправке исходного сообщения возникнет та же ошибка.</p></td>
</tr>
<tr class="odd">
<td><p>5.1.2</p></td>
<td><p><code>Invalid X.400 address</code></p></td>
<td><p>Получатель имеет адрес, отличный от SMTP, который не может быть сопоставлен с местом назначения. Адрес не является локальным, поэтому соединителей, настроенных для адресных пространств, содержащих адрес получателя, нет.</p></td>
<td><p>Убедитесь, что адрес получателя введен правильно. Если адрес получателя не относится к почтовой SMTP-системе, в которую доставляется электронная почта, необходимо добавить в топологию соответствующий тип соединителя и настроить его так, чтобы он обслуживал эту систему.</p></td>
</tr>
<tr class="even">
<td><p>5.1.3</p></td>
<td><p><code>Invalid recipient address</code></p></td>
<td><p>Это сообщение означает, что в сообщении указан неправильный адрес получателя.</p></td>
<td><p>Адрес получателя указан в неправильном формате, или его не удалось правильно сопоставить. Чтобы устранить эту ошибку, сначала проверьте адрес получателя и отправьте сообщение повторно.</p>
<p>Кроме того, проверьте политику получателей для протокола SMTP и убедитесь, что все домены почты, которые должны получать почту, указаны правильно.</p></td>
</tr>
<tr class="odd">
<td><p>5.1.4</p></td>
<td><p><code>Destination mailbox address ambiguous</code></p></td>
<td><p>Несколько получателей в организации Exchange имеют одинаковый адрес.</p></td>
<td><p>Эта ошибка обычно возникает из-за неправильной настройки доменных служб Active Directory. Возможно, из-за проблем с репликацией два объекта получателей в доменных службах Active Directory имеют одинаковый SMTP-адрес или адрес Exchange Server (EX).</p></td>
</tr>
<tr class="even">
<td><p>5.1.7</p></td>
<td><p><code>Invalid address</code></p></td>
<td><p>SMTP-адрес отправителя (атрибут <strong>mail</strong> в службе каталогов) указан неправильно или отсутствует. Сообщение невозможно доставить без допустимого атрибута <strong>mail</strong>.</p></td>
<td><p>Проверьте структуру каталогов отправителя и выясните, существует ли атрибут <strong>mail</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>5.2.1</p></td>
<td><p><code>Mailbox cannot be accessed</code></p></td>
<td><p>Не удается получить доступ к почтовому ящику. Возможно, почтовый ящик переведен в автономном режиме или отключен либо сообщение помещено на карантин в соответствии с правилом.</p></td>
<td><p>Проверьте, подключена ли база данных получателей, не отключен ли почтовый ящик получателя и не помещено ли на карантин сообщение.</p></td>
</tr>
<tr class="even">
<td><p>5.2.2</p></td>
<td><p><code>Mailbox full</code></p></td>
<td><p>Почтовый ящик получателя превысил свою квоту и не может принимать новые сообщения.</p></td>
<td><p>Эта ошибка возникает, когда почтовый ящик получателя превышает свою квоту хранилища. Для успешной доставки сообщения получатель должен уменьшить размер почтового ящика или администратор должен увеличить квоту хранилища.</p></td>
</tr>
<tr class="odd">
<td><p>5.2.3</p></td>
<td><p><code>Message too large</code></p></td>
<td><p>Сообщение слишком велико, превышена локальная квота. Например, для удаленного пользователя Exchange может быть задано ограничение на максимальный размер входящего сообщения.</p></td>
<td><p>Отправьте сообщение повторно без вложений или настройте серверное либо клиентское ограничение так, чтобы оно допускало доставку сообщений большего размера.</p></td>
</tr>
<tr class="even">
<td><p>5.2.4</p></td>
<td><p><code>Mailing list expansion problem</code></p></td>
<td><p>Получателем является неправильно настроенный динамический список рассылки. Или строка фильтра, или базовое различающееся имя динамического списка рассылки указаны неверно.</p></td>
<td><p>Задайте для классификатора хотя бы минимальный уровень ведения журнала событий и отправьте другое сообщение в динамический список рассылки. Проверьте, имеется ли в журнале событий приложений событие 6025 или 6026 со сведениями о том, какой атрибут объекта динамического списка рассылки настроен неправильно.</p></td>
</tr>
<tr class="odd">
<td><p>5.3.3</p></td>
<td><p><code>Unrecognized command</code></p></td>
<td><p>Когда на диске удаленного сервера Exchange заканчивается место для хранения почты, он может возвратить данный отчет о недоставке. Эта ошибка обычно возникает, когда отправляющий сервер отправляет почту с помощью команды ESMTP BDAT. Кроме того, она может свидетельствовать об ошибке протокола SMTP.</p></td>
<td><p>Убедитесь, что на удаленном сервере достаточно места для хранения почты. Проверьте журнал SMTP.</p></td>
</tr>
<tr class="even">
<td><p>5.3.4</p></td>
<td><p><code>Message too big for system</code></p></td>
<td><p>Сообщение превышает ограничение на размер сообщения, заданное для транспорта или базы данных почтовых ящиков, и его не удается принять. Этот сбой может вызваться отправляющей почтовой системой или системой получателя.</p></td>
<td><p>Эта ошибка возникает, когда размер отправленного сообщения превышает максимально допустимый размер сообщения при прохождении через компонент транспорта или базу данных почтовых ящиков. Для успешной доставки сообщения отправитель должен уменьшить его размер. Дополнительные сведения о настройке ограничений размера сообщений см. в разделе <a href="message-size-limits-exchange-2013-help.md">Ограничения на размер сообщений</a>.</p></td>
</tr>
<tr class="odd">
<td><p>5.3.5</p></td>
<td><p><code>System incorrectly configured</code></p></td>
<td><p>Обнаружена ситуация зацикливания почты; это означает, что сервер настроен так, что отправляет почту себе.</p></td>
<td><p>Проверьте наличие циклов в конфигурации соединителей сервера и убедитесь, что каждый соединитель определяется уникальным входящим портом. При наличии нескольких виртуальных серверов убедитесь, что ни один из них не находится в состоянии &quot;Все неназначенные&quot;.</p></td>
</tr>
<tr class="even">
<td><p>5.4.4</p></td>
<td><p><code>Invalid arguments</code></p></td>
<td><p>Данный отчет о недоставке возвращается, если отсутствует маршрут доставки сообщения или классификатор не может определить следующий сайте.</p></td>
<td><p>Убедитесь, что указано допустимое доменное имя и что существует запись MX.</p></td>
</tr>
<tr class="odd">
<td><p>5.4.6</p></td>
<td><p><code>Routing loop detected</code></p></td>
<td><p>Ошибка конфигурации привела к созданию почтового цикла. По умолчанию после 20 итераций цикла электронной почты Exchange прерывает цикл и создает отчет о недоставке для отправителя сообщения.</p></td>
<td><p>Эта ошибка возникает, когда при доставке сообщения создается другое сообщение. Это сообщение создает третье сообщение, и процесс повторяется, образуя цикл. Чтобы избежать исчерпания системных ресурсов, Exchange прерывает почтовый цикл после 20 итераций. Почтовые циклы обычно возникают из-за ошибки конфигурации на принимающем или отправляющем почтовом сервере (или обоих). Проверьте, включена ли автоматическая пересылка сообщений в конфигурации правил почтовых ящиков отправителя и получателя.</p></td>
</tr>
<tr class="even">
<td><p>5.5.2</p></td>
<td><p><code>Send hello first</code></p></td>
<td><p>Произошла общая ошибка SMTP при отправке команд SMTP вне последовательности. Например, сервер попытался отправить команду AUTH (авторизация), прежде чем идентифицировал себя с помощью команды EHLO.</p>
<p>Данная ошибка может также свидетельствовать о нехватке места на системном диске.</p></td>
<td><p>Просмотрите журнал SMTP или журнал средства Netmon и убедитесь в наличии достаточного места на диске и объема виртуальной памяти.</p></td>
</tr>
<tr class="odd">
<td><p>5.5.3</p></td>
<td><p><code>Too many recipients</code></p></td>
<td><p>Общее число получателей сообщения, указанных в полях &quot;Кому&quot;, &quot;Копия&quot; и &quot;СК&quot;, превышает общее количество получателей, допустимое для одного сообщения.</p></td>
<td><p>Эта ошибка происходит, если отправитель указывает слишком много получателей для сообщения. Для успешной доставки сообщения необходимо сократить количество адресов получателей сообщения или увеличить максимальное количество получателей.</p></td>
</tr>
<tr class="even">
<td><p>5.5.4</p></td>
<td><p><code>Invalid domain name</code></p></td>
<td><p>В сообщении используется неправильный формат адреса отправителя или получателя.</p>
<p>Одна из возможных причин этой проблемы заключается в том, что адрес получателя содержит знаки, не соответствующие стандартам Интернета.</p></td>
<td><p>Проверьте, не содержит ли адрес получателя нестандартные знаки.</p></td>
</tr>
<tr class="odd">
<td><p>5.5.6</p></td>
<td><p><code>Invalid message content</code></p></td>
<td><p>Данное сообщение свидетельствует о возможной ошибке протокола.</p></td>
<td><p>Проверьте журнал событий на наличие ошибок.</p></td>
</tr>
<tr class="even">
<td><p>5.7.1</p></td>
<td><p><code>Delivery not authorized</code></p></td>
<td><p>Отправителю не разрешено оправлять сообщения получателю.</p></td>
<td><p>Эта ошибка возникает, когда отправитель пытается отправить сообщение получателю, но не имеет на это разрешений. Это часто происходит при отправке сообщений в группу рассылки, которая принимает сообщения только от своих членов или других полномочных отправителей. Отправитель должен запросить разрешение на отправку сообщений получателю.</p>
<p>Эта ошибка также может возникать, если правило транспорта Exchange отклоняет сообщение из-за того, что оно соответствует настроенным условиям.</p></td>
</tr>
<tr class="odd">
<td><p>5.7.1</p></td>
<td><p><code>Unable to relay</code></p></td>
<td><p>Системе-отправителю запрещено отправлять сообщения в почтовую систему, которая не является конечным местом назначения сообщения электронной почты.</p></td>
<td><p>Эта ошибка возникает, когда отправляющая почтовая система пытается отправить анонимное сообщение в принимающую почтовую систему, а принимающая почтовая система не принимает сообщения для доменов, указанных для одного или нескольких получателей. Ниже перечислены наиболее распространенные причины этой ошибки.</p>
<ul>
<li><p>Сторонний пользователь пытается использовать почтовую систему получателя для отправки спама, и система отклоняет попытку. При отправке спама часто используется поддельный адрес электронной почты отправителя, поэтому отчет о недоставке мог быть отправлен на адрес электронной почты пользователя, который ничего не подозревает. Избежать этой ситуации трудно.</p></li>
<li><p>Запись MX для домена указывает на почтовую систему получателя, домен которой не является обслуживаемым. Администратор, отвечающий за определенное имя домена, должен исправить запись MX или настроить принимающую почтовую систему для приема сообщений, отправленных в этот домен (либо выполнить оба этих действия).</p></li>
<li><p>Отправляющая почтовая система или клиент, которые должны использовать принимающую почтовую систему для передачи сообщений, не имеют для этого правильных разрешений.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>5.7.1</p></td>
<td><p><code>Client was not authenticated</code></p></td>
<td><p>Отправляющая почтовая система не выполнила проверку подлинности для принимающей почтовой системы. Принимающая почтовая система требует проверки подлинности перед передачей сообщения.</p></td>
<td><p>Эта ошибка возникает в том случае, когда принимающий сервер должен пройти проверку подлинности перед передачей сообщения, а отправляющая почтовая система не выполнила проверку подлинности для принимающей почтовой системы. Администратор отправляющей системы должен настроить отправку почты с проверкой подлинности в принимающей почтовой системе для успешной доставки. Эта ошибка также может возникать при принятии анонимных сообщений из Интернета на сервере почтовых ящиков, не настроенном для этого.</p></td>
</tr>
<tr class="odd">
<td><p>5.7.3</p></td>
<td><p><code>Not Authorized</code></p></td>
<td><p>Отправитель запретил переназначение альтернативному получателю.</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


В начало

## Разделы отчета о недоставке

В Exchange 2013 отчеты о недоставке просты и понятны как для пользователей, так и для администраторов. Информация, отображаемая в отчете о недоставке, делится на следующие две области:

  - Раздел сведений для пользователя

  - Раздел сведений для администраторов

Сведения в каждом разделе предназначены для читателей этого раздела. Раздел сведений для пользователя идет первым, и в нем пользователю нетехническим языком объясняется, почему не удалось доставить сообщение. В разделе **Диагностические сведения для администраторов** содержатся подробные технические сведения, например заголовки исходных сообщений, которые помогают администраторам электронной почты устранить проблему с доставкой. На следующем рисунке показаны раздел сведений для пользователя и раздел **Диагностические сведения для администраторов**.

**Разделы отчета о недоставке**

![Отчет о недоставке с указанием сведений о диагностике для пользователя и администратора](images/Bb232118.96245455-5fb9-4669-a931-5563ddd3ab35(EXCHG.150).png "Отчет о недоставке с указанием сведений о диагностике для пользователя и администратора")

## Раздел сведений для пользователя

Раздел сведений для пользователя в отчете о недоставке, созданном Exchange, содержит информацию, которую необходимо сообщить пользователю, отправившему сообщение, которое не удалось доставить. Текст, который отображается в этом разделе, вставляется сервером Exchange, создавшим отчет о недоставке.

Текст в разделе сведений для пользователя должен помочь пользователям определить, почему сообщение отклонено и как отправить его повторно. Если возможно, в этом разделе указывается полное доменное имя сервера, который отклонил сообщение. Если не удается доставить сообщение нескольким получателям, указываются адреса электронной почты всех получателей, под которыми указывается причина ошибки.

Текст в разделе сведений для пользователя можно изменить с помощью командлета **New-SystemMessage**. Создав специальное сообщение, можно предоставить пользователям конкретную информацию, например телефонный номер для связи со службой технической поддержки или гиперссылку на справочные материалы для самостоятельного решения проблемы.

К началу

## Диагностические сведения для администраторов

В разделе **Диагностические сведения для администраторов** представлены более подробные сведения о конкретной ошибке, которая произошла при доставке сообщения, а также указан сервер, создавший отчет о недоставке, и сервер, отклонивший сообщение. В большинстве отчетов о недоставке присутствуют указанные ниже поля (они показаны на рис. "Разделы отчета о недоставке" выше в этом разделе).

  - **Формирующий сервер.** Формирующий сервер — это сервер SMTP, который создал отчет о недоставке. Формирующий сервер принимает расширенный код состояния (см. ниже). Этот код создает наглядный отчет о недоставке. Если удаленный сервер не указан после адреса электронной почты отправителя в разделе **Диагностические сведения для администраторов**, формирующий сервер также является сервером, который отклонил исходное сообщение электронной почты. Если не удается доставить сообщение, отправленное другому получателю в той же организации Exchange, обычно один и тот же сервер отклоняет исходное сообщение и создает отчет о недоставке.

  - **Отклоненный получатель**. Отклоненный получатель — это адрес электронной почты, на который не удалось доставить исходное сообщение. Если не удается доставить сообщение нескольким получателям, здесь перечисляются адреса электронной почты всех получателей. Это поле также содержит следующие дополнительные поля для каждого указанного адреса электронной почты:
    
      - **Удаленный сервер**   Это поле содержит полное доменное имя сервера, который отклоняет доставку сообщения в процессе сеансов связи SMTP. Поле "Удаленный сервер" заполняется только в том случае, когда была предпринята попытка доставки в удаленный домен, которая была отклонена до того, как принимающий сервер успешно подтвердил сообщение после отправки текста сообщения. Если исходное сообщение успешно подтверждается принимающим сервером, а затем отклоняется (например из-за ограничений для содержимого), поле "Удаленный сервер" не заполняется.
    
      - **Расширенный код состояния**. Расширенный код состояния — это код, возвращаемый сервером, который отклонил исходное сообщение. Расширенный код состояния указывает причину отклонения исходного сообщения. Он не перезаписывается Exchange, но используется для определения того, какой текст должен выводиться в разделе сведений для пользователей. Наиболее распространенные коды перечислены в разделе "Частые расширенные коды состояния" ниже в этой статье. Подробный список таких кодов можно найти в документе RFC 3463.
    
      - **Отклик SMTP**. Отклик SMTP — это текст, распознаваемый компьютером, который возвращается сервером, отклонившим исходное сообщение. Отклик SMTP обычно содержит короткое объяснение возвращенного расширенного кода состояния. Отклик SMTP не перезаписывается Exchange. Кроме того, этот отклик всегда представлен в кодировке US-ASCII.

  - **Исходные заголовки сообщения**. Раздел "Исходные заголовки сообщения" содержит заголовки отклоненных сообщений. Эти заголовки могут предоставлять важные диагностические сведения, например данные, которые помогут определить путь сообщения до его отклонения или то, соответствует ли поле **Кому** адресу электронной почты, указанному в поле отклоненного получателя.

В начало

## Примеры отчетов о недоставке

В следующих разделах приведены примеры двух способов создания отчетов о недоставке:

  - одним и тем же сервером;

  - различными серверами.

## Один и тот же сервер отклоняет сообщение и создает отчет о недоставке

В следующем примере показано, что происходит, когда удаленная организация электронной почты принимает доставку сообщения электронной почты через пограничный транспортный сервер, а затем отклоняет его из-за ограничения политики для почтового ящика получателя. В этом случае отправителю не разрешено оправлять сообщения получателю. Пограничные транспортные серверы не выполняют проверку размеров сообщений, поэтому в этом примере пограничный транспортный сервер принимает сообщение, так как оно имеет допустимый адрес получателя и не нарушает другие ограничения для содержимого. Так как удаленная организация электронной почты принимает все сообщение, включая его содержимое, она отвечает за отклонение сообщения и создание отчета о недоставке, который должен отправляться на сервер.

**Один и тот же сервер отклоняет сообщение и создает отчет о недоставке**

![Отчет о недоставке, в котором формирующий и отправляющий серверы совпадают](images/Bb232118.c9a7cd2d-f35f-4d77-8225-c29585fa3ccd(EXCHG.150).gif "Отчет о недоставке, в котором формирующий и отправляющий серверы совпадают")

Кроме того, сообщения, которые отклоняются при отправке получателям, входящим в ту же организацию Exchange, обычно отклоняются тем же почтовым сервером, который создает отчет о недоставке. Сообщения, которые отправляются локальным получателям, могут отклоняться по различным причинам, например из-за превышения квот почтовых ящиков, отсутствия прав на отправку сообщений получателю или сбоя оборудования, который приводит к продолжительной потере подключения к другим серверам в организации.

В обеих ситуациях удаленные серверы не включаются в список адресов электронной почты получателей в отчете о недоставке.

В начало

## Различные серверы отклоняют сообщение и создают отчет о недоставке

В следующем примере показано, что происходит, когда удаленная организация отклоняет доставку сообщения электронной почты даже до того, как она принимает сообщение. В этом примере удаленный сервер отклоняет сообщение и возвращает расширенный код состояния локальному отправляющему серверу, так как указанный получатель не существует. Отклонение происходит до того, как принимающий сервер подтверждает сообщение. Так как принимающий сервер не подтверждает сообщение, он отвечает за него. Поэтому локальный отправляющий сервер создает отчет о недоставке и отправляет его отправителю исходного сообщения.

**Различные серверы отклоняют сообщение и создают отчет о недоставке**

![Отчет о недоставке, в котором формирующий и отправляющий серверы различаются](images/Bb232118.adfb8d5a-9c1d-4cd9-8a71-ce14224434f8(EXCHG.150).gif "Отчет о недоставке, в котором формирующий и отправляющий серверы различаются")

В начало

## См. также


[Отчет о недоставке в Exchange Online и Office 365](https://go.microsoft.com/fwlink/p/?linkid=524931)
