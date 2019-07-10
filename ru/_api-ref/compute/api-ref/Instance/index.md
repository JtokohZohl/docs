---
editable: false
---

# Instance
Набор методов для управления ресурсами Instance.
## JSON-представление {#representation}
```json 
{
  "id": "string",
  "folderId": "string",
  "createdAt": "string",
  "name": "string",
  "description": "string",
  "labels": "object",
  "zoneId": "string",
  "platformId": "string",
  "resources": {
    "memory": "string",
    "cores": "string",
    "coreFraction": "string"
  },
  "status": "string",
  "metadata": "object",
  "bootDisk": {
    "mode": "string",
    "deviceName": "string",
    "autoDelete": true,
    "diskId": "string"
  },
  "secondaryDisks": [
    {
      "mode": "string",
      "deviceName": "string",
      "autoDelete": true,
      "diskId": "string"
    }
  ],
  "networkInterfaces": [
    {
      "index": "string",
      "macAddress": "string",
      "subnetId": "string",
      "primaryV4Address": {
        "address": "string",
        "oneToOneNat": {
          "address": "string",
          "ipVersion": "string"
        }
      },
      "primaryV6Address": {
        "address": "string",
        "oneToOneNat": {
          "address": "string",
          "ipVersion": "string"
        }
      }
    }
  ],
  "fqdn": "string",
  "schedulingPolicy": {
    "preemptible": true
  }
}
```
 
Поле | Описание
--- | ---
id | **string**<br><p>Идентификатор виртуальной машины.</p> 
folderId | **string**<br><p>Идентификатор каталога, которому принадлежит виртуальная машина.</p> 
createdAt | **string** (date-time)<br><p>Строка в формате <a href="https://www.ietf.org/rfc/rfc3339.txt">RFC3339</a>.</p> 
name | **string**<br><p>Имя виртуальной машины. Длина 1-63 символов.</p> 
description | **string**<br><p>Описание виртуальной машины. Длина описания должна быть от 0 до 256 символов.</p> 
labels | **object**<br><p>Метки ресурса в формате <code>key:value</code>. Максимум 64 на ресурс.</p> 
zoneId | **string**<br><p>Идентификатор зоны доступности, где находится виртуальная машина.</p> 
platformId | **string**<br><p>Идентификатор аппаратной платформы виртуальной машины.</p> 
resources | **object**<br><p>Вычислительные ресурсы виртуальной машины, такие как объем памяти и количество ядер.</p> 
resources.<br>memory | **string** (int64)<br><p>Объем памяти в байтах, доступный виртуальной машине.</p> 
resources.<br>cores | **string** (int64)<br><p>Количество ядер, доступных виртуальной машине.</p> 
resources.<br>coreFraction | **string** (int64)<br><p>Базовый уровень производительности CPU с возможностью повышения производительности выше этого уровня. Это поле устанавливает базовую производительность для каждого ядра.</p> 
status | **string**<br><p>Статус виртуальной машины.</p> <ul> <li>PROVISIONING: Виртуальная машина ожидает выделения ресурсов.</li> <li>RUNNING: Виртуальная машина работает нормально.</li> <li>STOPPING: Виртуальная машина останавливается.</li> <li>STOPPED: Виртуальная машина остановлена.</li> <li>STARTING: Виртуальная машина запускается.</li> <li>RESTARTING: Виртуальная машина перезапускается.</li> <li>UPDATING: Виртуальная машина обновляется.</li> <li>ERROR: С виртуальной машиной произошла ошибка, блокирующая работу.</li> <li>CRASHED: Виртуальная машина аварийно завершила работу и будет перезапущена автоматически.</li> <li>DELETING: Виртуальная машина удаляется.</li> </ul> 
metadata | **object**<br><p>Метаданные в формате пар <code>key:value</code>, назначаемые данной виртуальной машине. Это включает произвольные пользовательские метаданные и предзаданные ключи.</p> <p>Например, можно использовать метаданные для доставки открытого ключа SSH на виртуальную машину. Дополнительные сведения см. в разделе <a href="/docs/compute/concepts/vm-metadata">Метаданные виртуальной машины</a>.</p> 
bootDisk | **object**<br><p>Загрузочный диск, подключенный к виртуальной машине.</p> 
bootDisk.<br>mode | **string**<br><p>Режим доступа к ресурсу Disk.</p> <ul> <li>READ_ONLY: Доступ на чтение.</li> <li>READ_WRITE: Доступ на чтение и запись.</li> </ul> 
bootDisk.<br>deviceName | **string**<br><p>Cерийный номер, который на виртуальной машине с операционной системой Linux отображается в директории /dev/disk/by-id/.</p> <p>Это значение может использоваться для ссылки на устройство внутри виртуальной машины при монтировании, изменении размера и т. д.</p> 
bootDisk.<br>autoDelete | **boolean** (boolean)<br><p>Указывает, должен ли диск автоматически удалиться при удалении виртуальной машины.</p> 
bootDisk.<br>diskId | **string**<br><p>Идентификатор диска, подключенного к виртуальной машине.</p> 
secondaryDisks[] | **object**<br><p>Массив дополнительных дисков, подключенных к виртуальной машине.</p> 
secondaryDisks[].<br>mode | **string**<br><p>Режим доступа к ресурсу Disk.</p> <ul> <li>READ_ONLY: Доступ на чтение.</li> <li>READ_WRITE: Доступ на чтение и запись.</li> </ul> 
secondaryDisks[].<br>deviceName | **string**<br><p>Cерийный номер, который на виртуальной машине с операционной системой Linux отображается в директории /dev/disk/by-id/.</p> <p>Это значение может использоваться для ссылки на устройство внутри виртуальной машины при монтировании, изменении размера и т. д.</p> 
secondaryDisks[].<br>autoDelete | **boolean** (boolean)<br><p>Указывает, должен ли диск автоматически удалиться при удалении виртуальной машины.</p> 
secondaryDisks[].<br>diskId | **string**<br><p>Идентификатор диска, подключенного к виртуальной машине.</p> 
networkInterfaces[] | **object**<br><p>Массив сетевых интерфейсов, присоединенных к виртуальной машине.</p> 
networkInterfaces[].<br>index | **string**<br><p>Индекс сетевого интерфейса, генерируемого сервером, 0,1,2... В настоящее время для каждой виртуальной машины поддерживается только один сетевой интерфейс.</p> 
networkInterfaces[].<br>macAddress | **string**<br><p>MAC-адрес, назначенный сетевому интерфейсу.</p> 
networkInterfaces[].<br>subnetId | **string**<br><p>Идентификатор подсети.</p> 
networkInterfaces[].<br>primaryV4Address | **object**<br><p>Основной IPv4-адрес, который назначен виртуальной машине для данного сетевого интерфейса.</p> 
networkInterfaces[].<br>primaryV4Address.<br>address | **string**<br><p>Внутренний IPv4-адрес, назначенный виртуальной машине для этого сетевого интерфейса.</p> 
networkInterfaces[].<br>primaryV4Address.<br>oneToOneNat | **object**<br><p>Конфигурация One-to-one NAT . Если отсутствует, NAT не был настроен.</p> 
networkInterfaces[].<br>primaryV4Address.<br>oneToOneNat.<br>address | **string**<br><p>Публичный IP-адрес, связанный с данной виртуальной машиной</p> 
networkInterfaces[].<br>primaryV4Address.<br>oneToOneNat.<br>ipVersion | **string**<br><p>Версия IP для публичного IP-адреса.</p> <ul> <li>IPV4: IPv4-адрес, например 192.0.2.235.</li> <li>IPV6: Адрес IPv6. На данный момент не доступен.</li> </ul> 
networkInterfaces[].<br>primaryV6Address | **object**<br><p>Основной IPv6-адрес, который назначен виртуальной машине для данного сетевого интерфейса. IPv6 еще не доступен.</p> 
networkInterfaces[].<br>primaryV6Address.<br>address | **string**<br><p>Внутренний IPv4-адрес, назначенный виртуальной машине для этого сетевого интерфейса.</p> 
networkInterfaces[].<br>primaryV6Address.<br>oneToOneNat | **object**<br><p>Конфигурация One-to-one NAT . Если отсутствует, NAT не был настроен.</p> 
networkInterfaces[].<br>primaryV6Address.<br>oneToOneNat.<br>address | **string**<br><p>Публичный IP-адрес, связанный с данной виртуальной машиной</p> 
networkInterfaces[].<br>primaryV6Address.<br>oneToOneNat.<br>ipVersion | **string**<br><p>Версия IP для публичного IP-адреса.</p> <ul> <li>IPV4: IPv4-адрес, например 192.0.2.235.</li> <li>IPV6: Адрес IPv6. На данный момент не доступен.</li> </ul> 
fqdn | **string**<br><p>Доменное имя виртуальной машины. FQDN определяется сервером в формате <code>&lt;hostname&gt;.&lt;region_id&gt;.internal</code> при создании виртуальной машины. Если имя хоста не было указано при создании виртуальной машины, FQDN будет <code>&lt;id&gt;.auto.internal</code>.</p> 
schedulingPolicy | **object**<br><p>Политика планирования.</p> 
schedulingPolicy.<br>preemptible | **boolean** (boolean)<br><p>Если значение равно true — будет создана прерываемая виртуальная машина. Дополнительные сведения см. в разделе <a href="/docs/compute/concepts/preemptible-vm">Прерываемые виртуальные машины</a>.</p> 

## Методы {#methods}
Метод | Описание
--- | ---
[attachDisk](attachDisk.md) | Присоединяет диск к виртуальной машине.
[create](create.md) | Создает виртуальную машину в указанном каталоге. Метод запускает асинхронную операцию, которую можно отменить перед тем, как она завершится.
[delete](delete.md) | Удаляет указанную виртуальную машину.
[detachDisk](detachDisk.md) | Отсоединяет диск от виртуальной машины.
[get](get.md) | Возвращает указанный ресурс Instance.
[getSerialPortOutput](getSerialPortOutput.md) | Возвращает вывод последовательного порта указанного ресурса Instance.
[list](list.md) | Возвращает список доступных ресурсов Instance в указанном каталоге.
[listOperations](listOperations.md) | Возвращает список операций для указанной виртуальной машины.
[restart](restart.md) | Перезапускает работающую виртуальную машину.
[start](start.md) | Запускает остановленную виртуальную машину.
[stop](stop.md) | Останавливает запущенную виртуальную машину.
[update](update.md) | Изменяет указанную виртуальную машину.
[updateMetadata](updateMetadata.md) | Обновляет метаданные указанной виртуальной машины.