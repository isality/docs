{% list tabs %}

* Managed Kafka

    Подключение к БД с указанием идентификатора кластера в {{ yandex-cloud }}. Доступно только для кластеров, развернутых в сервисе [{{ mkf-name }}](../../../managed-kafka/).

    Для подключения задайте обязательные параметры:

    * **Managed Kafka** — выберите кластер, к которому необходимо подключиться.
    * **Аутентификация** — укажите имя и пароль учетной записи, от имени которой сервис {{ data-transfer-name }} будет подключаться к топику.
    * {% include [Field Topic](../fields/topic.md) %}

* On Premise

    Подключение к топику с явным указанием сетевых адресов хостов-брокеров.

    Для подключения задайте обязательные параметры:

    * **On Premise**:
        * **Адреса брокеров** — укажите IP-адреса или FQDN хостов-брокеров.

            Если номер порта {{ KF }} отличается от стандартного, укажите его через двоеточие после имени хоста:

            ```text
            <IP-адрес или FQDN хоста-брокера>:<номер порта>
            ```

        * **SSL** — использовать шифрование для защиты соединения.
        * **PEM-сертификат** — если требуется шифрование передаваемых данных, например для соответствия требованиям [PCI DSS]({{ link-pci-dss-ru }}), загрузите файл [сертификата](../../../managed-kafka/operations/connect.md#get-ssl-cert) или добавьте его содержимое в текстовом виде.

    * **Аутентификация** — при выборе значения `SASL` укажите имя учетной записи, пароль и механизм хеширования.
    * {% include [Field Topic](../fields/topic.md) %}

{% endlist %}
