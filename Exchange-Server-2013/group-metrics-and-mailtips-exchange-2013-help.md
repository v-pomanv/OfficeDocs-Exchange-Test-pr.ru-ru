﻿---
title: 'Показатели группы и подсказки: Exchange 2013 Help'
TOCTitle: Показатели группы и подсказки
ms:assetid: 74a55072-4ba9-45bb-a18f-41afbf3de30b
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ674302(v=EXCHG.150)
ms:contentKeyID: 50488230
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Показатели группы и подсказки

 

_**Применимо к:**Exchange Server 2013_

_**Последнее изменение раздела:**2012-10-16_

Групповые метрики — это набор данных о группах рассылки и динамических группах рассылки в организации, таких как:

  - Количество участников

  - Количество внешних участников организации

Данные групповых метрик используются для поддержки подсказок в системе Microsoft Exchange Server 2013. Подсказки — это информационные сообщения, которые отображаются для отправителей во время создания сообщений. Дополнительные сведения о подсказках, включая полный список доступных подсказок в Exchange 2013, см. в разделе [MailTips](mailtips-exchange-2013-help.md).

Данные групповых метрик используются следующими подсказками:

  - **Большая аудитория**   Эта подсказка отображается, когда отправитель добавляет группу рассылки, количество участников группы которой является большой аудиторией, согласно конфигурации организации. По умолчанию любое сообщение, адресованное более 25 участникам, считается большой аудиторией.

  - **Внешние получатели**   Эта подсказка отображается, когда отправитель добавляет группу рассылки с внешними участниками организации.

Подсказки проверяются каждый раз, когда отправитель добавляет получателя в сообщение. Чтобы получить эту информацию, Exchange вычисляет данные групповых метрик в фоновом процессе, для которого можно запланировать время запуска за пределами регулярного рабочего времени в организации. При оценке получателей в подсказках Exchange считывает данные групповых метрик.

## Создание групповых метрик

В Exchange 2013 данные групповых метрик хранятся в атрибутах **msExchGroupMemberCount** и **msExchGroupExternalMemberCount** объекта группы в Active Directory. Следующие файлы в папке %ExchangeInstallPath%GroupMetrics также связаны с групповыми метриками:

  - **Cookie\_*\<nnnnnnnn\>*.dsc**   В этом текстовом файле содержатся сведения о сервере почтовых ящиков, который служит для создания данных групповых метрик, а также последнее время успешного создания групповых метрик. Это позволяет создавать данные групповых метрик для групп, которые были изменены с момента последнего создания групповых метрик.

  - **ChangedGroups.txt**   В этом файле содержится список групп, обновленных во время последнего создания данных групповых метрик.

Создание групповых метрик ведется почтовым ящиком арбитража, называемым также почтовым ящиком организации. Когда параметр *GMGen* почтового ящика арбитража равен `$true`, почтовый ящик отвечает за создание данных групповых метрик.

Сервер почтовых ящиков создает полные данные групповых метрик для всех групп рассылки и динамических групп рассылки в первый раз, когда запускается помощник по обслуживанию почтовых ящиков, а также выполняет дополнительные обновления для всех групп, которые были изменены со времени последнего полного создания. По умолчанию данные групповых метрик создаются ежедневно в случайное время, когда сервер Exchange не загружен. Если рабочая нагрузка постоянно высока, создание групповых метрик может быть пропущено.

Чтобы настроить создание групповых метрик, см. раздел [Настройка показателей группы](configure-group-metrics-exchange-2013-help.md).
