﻿---
title: 'Служба доступности в Exchange 2013: Exchange 2013 Help'
TOCTitle: Служба доступности в Exchange 2013
ms:assetid: 9722dea2-2bf8-437c-85c0-3ab65b8a07b9
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb232134(v=EXCHG.150)
ms:contentKeyID: 52061245
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Служба доступности в Exchange 2013

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2016-12-09_

Служба доступности Exchange 2013 предоставляет клиентам Майкрософт Outlook и Outlook Web App доступ к сведениям о доступности. Служба доступности расширяет для специалистов по обработке данных возможности ведения календаря и планирования собраний и предоставляет безопасные, согласованные и обновленные сведения о доступности.

Outlook и Outlook Web App используют службу доступности для выполнения следующих задач:

  - получение текущих сведений о занятости для почтовых ящиков Exchange 2013

  - получение текущих сведений о занятости из других организаций Exchange 2013

  - получение опубликованных сведений о занятости из общих папок для почтовых ящиков на серверах, на которых установлены предыдущие версии Exchange

  - просмотр рабочих часов участников

  - отображение предложений по времени проведения собраний

**Содержание**

Обзор службы доступности

Сведения о состоянии "Нет на месте"

API-интерфейс службы доступности

Балансировка сетевой нагрузки службы доступности

Способы получения сведений о занятости

## Обзор службы доступности

Служба доступности получает сведения о доступности непосредственно из целевых почтовых ящиков пользователей Exchange 2013, Exchange 2010 и Exchange 2007. Ее можно также настроить для получения сведений о доступности пользователей более ранних версий Exchange. В топологиях с почтовыми ящиками Exchange 2007, Exchange 2010 и Exchange 2013, в которых все клиенты используют приложение Outlook 2007 и более поздние версии, служба доступности позволяет получать сведения о доступности.

Outlook использует службу автообнаружения Exchange для получения URL-адреса службы доступности. Дополнительные сведения о службе автообнаружения см. в разделе [Служба автообнаружения](autodiscover-service-for-exchange-2013.md).

Настроить службу доступности можно с помощью командной консоли Exchange. Нельзя настроить службу доступности с помощью Центра администрирования Exchange (EAC).

## Сведения о состоянии "Нет на месте"

Служба доступности предоставляет также доступ к автоматическим ответам, отправляемым пользователями во время их отсутствия на работе в течение определенного времени.

Специалисты по обработке данных могут использовать функцию автоматических ответов (ранее называлась "Отсутствие на рабочем месте") в приложениях Outlook и Outlook Web App, чтобы оповестить других пользователей о том, что они не смогут отвечать на сообщения электронной почты. Эта функция упрощает установку автоматических ответов и управление ими для специалистов по обработке данных и администраторов.

## API-интерфейс службы доступности

Служба доступности является частью программного интерфейса Exchange 2013. Она доступна как веб-служба, которая позволяет разработчикам создавать сторонние средства интеграции.

## Балансировка сетевой нагрузки службы доступности

С помощью функции балансировки сетевой нагрузки (NLB) на серверах клиентского доступа, на которых запущена служба доступности, можно повысить производительность и надежность работы пользователей, учитывающих сведения о занятости. Outlook позволяет находить URL-адрес службы доступности с помощью службы автообнаружения. Чтобы использовать функцию балансировки сетевой нагрузки в службе доступности, необходимо изменить конфигурацию.

Внутренний URL-адрес используется для доступа из интрасети, а внешний URL-адрес — для доступа из Интернета. При необходимости использовать один URL-адрес для внутреннего и для внешнего трафика убедитесь, что служба доменных имен (DNS) правильно настроена для маршрутизации внутреннего трафика на внутренний URL-адрес напрямую. Убедитесь также, что доступ к URL-адресу возможен как из внутренней сети, так и из внешней. Для работы служб автообнаружения и доступности необходимо настроить службу DNS таким образом, чтобы mail.\<*имя\_домена*\>.com и autodiscover.mail.\<*имя\_домена*\>.com указывали на виртуальный IP-адрес (VIP) вашего решения балансировки нагрузки, где \<*имя\_домена*\> — имя вашего домена.

> [!NOTE]  
> Дополнительные сведения см. в разделах <a href="https://go.microsoft.com/fwlink/p/?linkid=45959">Технический справочник по балансировке сетевой нагрузки</a> и <a href="https://go.microsoft.com/fwlink/p/?linkid=49315">Кластеры балансировки сетевой нагрузки</a>. Кроме того, вы можете просмотреть веб-сайты сторонних компаний, посвященные программному обеспечению балансировки нагрузки.


## Способы получения сведений о занятости

В следующей таблице перечислены способы получения сведений о занятости в различных топологиях с одним лесом.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Клиент</th>
<th>Запущен почтовый ящик, получающий сведения о занятости</th>
<th>Запущен целевой почтовый ящик</th>
<th>Способ получения сведений о занятости</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>Exchange 2013, Exchange 2010 или Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 или Exchange 2007</p></td>
<td><p>Служба доступности считывает сведения о занятости из целевого почтового ящика.</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 или Exchange 2007</p></td>
<td><p>Exchange 2010 или Exchange 2007</p></td>
<td><p>Служба доступности считывает сведения о занятости из целевого почтового ящика.</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2010 или Exchange 2007</p></td>
<td><p>Exchange 2003</p></td>
<td><p>Служба доступности устанавливает HTTP-подключение к виртуальному каталогу /public почтового ящика Exchange 2003.</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013, Exchange 2010 или Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 или Exchange 2007</p></td>
<td><p>Приложение Outlook Web App в Exchange 2010 или Outlook Web Access в Exchange 2007 вызывает интерфейс API службы доступности, который считывает сведения о доступности из целевого почтового ящика.</p></td>
</tr>
</tbody>
</table>

