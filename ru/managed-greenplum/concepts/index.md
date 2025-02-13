# Взаимосвязь ресурсов сервиса

Основная сущность, которой оперирует сервис {{ mgp-name }} — _кластер баз данных_.

Каждый кластер состоит из хостов баз данных — виртуальных машин с развернутыми серверами СУБД. Кластер {{ mgp-name }} включает:

* один или два _хоста-мастера_;
* два или больше _хостов-сегментов_.

Если в кластере два хоста-мастера, один из них становится _первичным_ (PRIMARY), а другой — _резервным_ (STANDBY).

Первичный мастер принимает клиентские подключения и SQL-запросы и распределяет обработку запросов по хостам-сегментам. Резервный мастер непрерывно реплицирует данные первичного и пользовательских подключений не принимает. Одиночный хост-мастер всегда является первичным.

На хостах-сегментах развернуты самостоятельные СУБД (_сегменты_), которые хранят части данных и исполняют большинство операций по обработке запросов. Каждый сегмент в кластере имеет одну реплику — зеркальный сегмент, который находится на другом хосте и хранит копию данных с основного сегмента.

Все хосты кластера {{ mgp-name }} размещаются в одной зоне доступности. [Подробнее о географии {{ yandex-cloud }}](../../overview/concepts/geo-scope.md).

Кластер {{ mgp-name }} с двумя хостами-мастерами в случае отказа одного из них продолжает обрабатывать запросы. Кластер с единственным хостом-мастером отказоустойчивости не обеспечивает.

Виртуальные машины, соответствующие хостам кластера, могут размещаться:

- На _стандартных хостах_ {{ yandex-cloud }}.

    Это физические серверы для размещения виртуальных машин кластера. Такие хосты выбираются случайным образом из пула доступных хостов, удовлетворяющих выбранной конфигурации кластера.

- На _выделенных хостах_ {{ yandex-cloud }}.

    Это физические серверы для размещения исключительно ваших виртуальных машин. Эти виртуальные машины обеспечивают как работу кластера, так и работу других ваших сервисов, которые поддерживают выделенные хосты. Такие хосты выбираются из _групп выделенных хостов_, указанных при создании кластера.

    При таком варианте размещения обеспечивается физическая изоляция виртуальных машин. Кластер {{ mkf-name }}, использующий выделенные хосты, обладает всеми возможностями обычных кластеров.

    Подробнее см. в разделе [{#T}](../../compute/concepts/dedicated-host.md).

При создании кластера необходимо указывать:

* _Класс хостов_ — шаблон виртуальной машины, по которому будут развертываться хосты кластера. Список доступных классов и их характеристики см. в разделе [{#T}](instance-types.md).

* _Окружение_ — среду, в которой будет развертываться кластер:
    * `PRODUCTION` — для стабильных версий ваших приложений.
    * `PRESTABLE` — для тестирования, в том числе самого сервиса {{ mgp-short-name }}. В Prestable-окружении раньше появляются новые возможности, улучшения и исправления ошибок. При этом не все обновления обеспечивают обратную совместимость.

{% include [monitoring-access](../../_includes/mdb/monitoring-access.md) %}

{% include [greenplum-trademark](../../_includes/mdb/mgp/trademark.md) %}
