﻿---
title: 'Exchange 2013: выпуски и версии: Exchange 2013 Help'
TOCTitle: 'Exchange 2013: выпуски и версии'
ms:assetid: b563b543-fb3f-4465-9a54-cbfd680aee1f
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb232170(v=EXCHG.150)
ms:contentKeyID: 50556474
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013: выпуски и версии

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2016-12-09_

Сервер Microsoft Exchange Server 2013 поставляется в двух выпусках: Standard Edition и Enterprise Edition. Выпуск Enterprise Edition может расширяться до 50 подключенных баз данных на сервер в RTM-версии и CU1-версии и до 100 подключенных баз данных на сервер в CU2-версии и в последующих версиях; выпуск Standard Edition ограничен 5 подключенными базами данных на сервер. Подключенная база данных — это база данных, которая находится в использовании. Подключенная база данных может быть активной базой данных почтовых ящиков, предназначенной для использования клиентами, или пассивной базой данных почтовых ящиков, подключаемой в процессе восстановления для репликации и преобразования журналов. Хотя можно создавать базы данных сверх приведенных выше ограничений, подключать можно только указанное максимальное количество. В этих ограничениях не учитывается база данных восстановления.

Выпуски отличаются условиями лицензирования и определяются ключом продукта. При вводе действительного ключа лицензии продукта происходит установка поддерживаемого выпуска сервера. Ключи продукта можно использовать только для замены ключа на ключ для того же выпуска продукта и для обновления, но не для перехода на использование более ранней версии. Действительный ключ продукта можно использовать для перехода с пробного выпуска Exchange 2013 на выпуск Standard Edition или Enterprise Edition. Действительный ключ продукта также можно использовать для перехода с выпуска Standard Edition на выпуск Enterprise Edition.

С помощью ключа продукта того же выпуска можно лицензировать сервер. Например, если для установки двух серверов Standard Edition с двумя ключами по ошибке был использован только один из ключей, можно изменить ключ для одного из серверов на второй выданный ключ. Для этого не требуется переустановка или изменение конфигурации. После ввода ключа продукта и перезапуска службы банка данных Microsoft Exchange будет использоваться выпуск, соответствующий ключу продукта.

После истечения срока действия пробного выпуска сервер продолжает работу в обычном режиме, поэтому можно использовать пробный выпуск Exchange 2013 для лабораторий, учебных заведений и в демонстрационных целях по истечении 120 дней без необходимости его переустановки.

Как упоминалось ранее, нельзя использовать ключи продукта для перехода на использование более ранней версии (с выпуска Enterprise Edition на выпуск Standard Edition или с любого выпуска на пробный выпуск). Для этого потребуется удалить Exchange 2013, установить Exchange 2013 повторно и ввести правильный ключ продукта.

## Версии Exchange 2013

Список версий Exchange 2013 и сведения о загрузке и установке последней версии Exchange 2013 см. в следующих разделах:

  - [Обновления для Exchange Server: номера сборок и даты выпуска](https://technet.microsoft.com/ru-ru/library/hh135098\(v=exchg.150\))

  - [Обновление Exchange 2013 с помощью последнего накопительного или обычного пакета обновления](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)

Чтобы просмотреть номер сборки своей версии Exchange 2013, выполните следующую команду в командной консоли Exchange:

    Get-ExchangeServer | fl name,edition,admindisplayversion

## Типы лицензий Exchange 2013

Exchange 2013 лицензируется с помощью модели серверных или клиентских (CAL) лицензий аналогично Exchange 2010. Существуют следующие типы лицензий:

  - **Серверные лицензии**.   Лицензия должна быть назначена каждому экземпляру программного обеспечения сервера, которое запущено. Серверная лицензия продается в двух выпусках сервера: Standard Edition и Enterprise Edition.

  - **Клиентские лицензии (CAL)**. Exchange 2013 также поставляется в двух выпусках с клиентскими лицензиями, которые называются Standard CAL и Enterprise CAL. Можно использовать различные сочетания серверных выпусков и типов CAL. Например, можно использовать клиентские лицензии Enterprise CAL с выпуском сервера Exchange 2013 Standard Edition. Аналогично можно использовать клиентские лицензии Standard CAL с выпуском Exchange 2013 Enterprise Edition.

Дополнительные сведения о типах лицензии Exchange см. в статье [Лицензирование](https://go.microsoft.com/fwlink/p/?linkid=392675).

