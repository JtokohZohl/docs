# Настройка сети для {{ dataproc-name }}

Согласно [концецпии](https://cloud.yandex.ru/docs/vpc/concepts/network) сети в Яндекс.Облаке, хосты без публичных IP-адресов в кластере {{ dataproc-name }} не имеют доступа к ресурсам, находящимся за пределами виртуальной сети {{vpc-short-name}}. Чтобы взаимодействовать с узлами других сетей, интерфейсами сервисов Яндекс.Облака или узлами в интернете необходимо настроить публичный IP-адрес для хоста или воспользоваться NAT в интернет для нужной подсети.

### NAT в интернет

Возможность настроить NAT в интернет для подсетей {{ vpc-short-name }} находится на стадии Preview. Чтобы запросить доступ к ней:
 
1. Войдите в [консоль управления]({{ link-console-main }}).
1. Выберите сервис {{ vpc-short-name }} в нужном каталоге.
1. Нажмите на строку нужной виртуальной сети.
1. Нажмите значок ![options](../../_assets/options.svg) в строке подсети и выберите пункт **Включить NAT в интернет**.

   ![image](../../_assets/mdb/enable_egress_nat.png)
   
Откроется форма, из которой вы сможете отправить заявку на доступ к возможности.

### Использование NAT и статических маршрутов

В NAT-конфигурации весь трафик проходит через дополнительную виртуальную машину (NAT-инстанс):

* Вы можете контролировать весь исходящий трафик, и при необходимости развернуть не только NAT, но и VPN между подсетью Облака и нужными ресурсами.
* При этом возникают дополнительные затраты на NAT-инстанс, и может оказаться существенным ограничение в пропускной способности одного порта виртуальной машины.

Чтобы воспользоваться NAT-конфигурацией вам понадобится две виртуальных сети: одна с кластерами {{ dataproc-name }}, и вторая с виртуальной машиной, которой присвоен публичный IP-адрес.

Примеры сетей:
- `dataproc-net` - сеть с кластерами {{ dataproc-name }} и CIDR `192.168.1.0/24`.
- `dataproc-nat-net` - сеть для NAT-инстанса и CIDR `192.168.100.0/24`.

Чтобы из сети `dataproc-net` появился доступ к внешним ресурсам:

1. Создайте в сети `dataproc-nat-net` виртуальную машину на основе Ubuntu 18.04 с публичным IP-адресом.
2. Скопируйте внутренний IP-адрес созданной машины.
2. На странице сети `dataproc-nat-net` создайте таблицу маршрутизации с именем `nat`.
3. В таблицу маршрутизации добавьте статический маршрут:
   * **Префикс назначения** — `0.0.0.0/0`
   * **Next hop**: <внутренний IP-адрес NAT-инстанса>
4. На странице сети привяжите таблицу маршрутизации `nat` к сети `dataproc-net`.
5. Включите маршрутизацию на NAT-инстансе, дописав следующие строки в файл `/etc/sysctl.conf`:
   ```(ini)
   net.ipv4.ip_forward = 1
   net.ipv4.conf.all.accept_redirects = 1
   net.ipv4.conf.all.send_redirects = 1
   ```
1. Включите исполнение `/etc/rc.local` на запуске, выполнив команды:

   ```bash
   $ sudo systemctl enable rc-local
   $ sudo touch /etc/rc.local
   $ sudo chmod 755 /etc/rc.local
   ```
1. В файл `/etc/rc.local` допишите следующий код:

   ```bash
   #!/bin/sh
   
   iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
   ```
1. Перезапустите виртуальную машину:

   ```bash
   $ sudo reboot -f
   ```

Чтобы проверить, правильно ли настроен NAT, выполните на виртуальной машине в сети `dataproc-net` следующую команду:

```bash
$ curl ifconfig.co
```

При корректной конфигурации команда выведет публичный IP-адрес NAT-инстанса.
