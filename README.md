# Reflection
DDOSPOT — это «платформа-приманка» для отслеживания и мониторинга распределенных атак типа «отказ в обслуживании » (DDoS) на основе UDP. В настоящее время платформа поддерживает следующие сервисы в виде относительно простых плагинов, называемых pots :

1) DNS
2) NTP
3) SSDP

# Плагины
Все плагины имеют одинаковую общую структуру (в pots/каталоге), могут быть настроены через специальный файл конфигурации и хранить информацию о запросах (например, атаках или сканированиях ) в соответствующей базе данных и файле журнала. Каждый плагин использует отдельную базу данных (в db/каталоге) и выделенный файл журнала (в logs/каталоге) и имеет возможность генерировать ежедневный набор IP-адресов, которые можно считать злоумышленниками/сканерами — эти черные списки хранятся в bl/каталоге. Кроме того, каждый плагин может отправлять уведомления по электронной почте, когда начинается атака на определенную страну.

Краткая информация о доступных в настоящее время плагинах приведена в разделах ниже.

# DNS
Плагин DNS основан на UDPot и использует Twisted framework/engine. Он пытается максимально точно эмулировать реальную службу DNS, перенаправляя все запросы действительному рекурсивному преобразователю и возвращая произвольный ответ на запрос CHAOS. Таким образом, коэффициент усиления зависит от возвращаемого ответа.

# NTP
Отвечает на 3 режима пакетов NTP:

1) Клиент (режим 3)
2) Контроль (режим 6)
3) monlist (режим 7)

Эти режимы были выбраны потому, что они чаще всего используются в DDoS-атаках на основе усиления на NTP (режим 6 и 7), а клиентский режим был реализован для того, чтобы служба выглядела более реалистично. Все переменные клиента NTP для этих режимов полностью настраиваются (например, скачок, задержка, точность и т. д.). Список monlist одноранговых узлов и информация об этих одноранговых узлах могут быть сгенерированы случайным образом или с использованием предоставленного фиксированного списка. Коэффициент усиления можно настроить, потому что он напрямую зависит от количества определенных пиров.

# SSDP
Отвечает на действительные M-SEARCHзапросы многоадресной рассылки ( ) и обеспечивает (чрезвычайно ограниченную и легкую) эмуляцию MiniUPnP . Как и NTP, он полностью настраиваемый — коэффициент усиления зависит от количества определенных UPnP-устройств и их данных, указанных в конфигурации.

# Установка
Для DDOSPOT требуется Python 3 и несколько дополнительных пакетов (я запускал у себя на python 3.8):

1) colorama
2) hpfeeds
3) python-geoip
4) python-geoip-geolite2
5) schedule
6) SQLAlchemy
7) tabulate
8) Twisted


