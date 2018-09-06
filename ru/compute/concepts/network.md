# Сеть на виртуальной машине

При создании виртуальной машины необходимо задать настройки сетевого интерфейса, подключенного к ней: выбрать [подсеть](../../vpc/concepts/network.md#subnet), к которой будет подключена виртуальная машина, настроить [внутренний](#internal-ip) и [внешний IP-адрес](#external-ip). Это позволит виртуальной машине взаимодействовать с другими сервисами во внутренней сети и в сети Интернет.

После подключения сетевого интерфейса виртуальной машине будет присвоен внутренний IP-адрес в подсети и [FQDN](#hostname). Внешний IP-адрес будет присвоен только если это было указано при создании виртуальной машины.

> [!NOTE]
> Настройка сетевого интерфейса доступна только при создании виртуальной машины. Например, подключить виртуальную машину к другой подсети после создания невозможно.

IP-адреса, FQDN и другую информацию можно узнать в консоли управления в блоке **Сети и доступы** на странице виртуальной машины. Эти данные можно использовать для подключения к виртуальной машине.

На виртуальных машинах, созданных из публичных образов Linux, IP-адрес и имя хоста (FQDN) не прописываются автоматически в файл `/etc/hosts`. В некоторых случаях это может повлиять на работу команды `sudo`.

## Внутренний IP-адрес {#internal-ip}

Вы можете указать внутренний IP-адрес, по которому будет доступна виртуальная машина после создания. Если внутренний IP-адрес не был указан, то он будет назначен автоматически.

> [!NOTE]
> На данный момент поддерживаются только IPv4-адреса.

Внутренний IP-адрес можно использовать для доступа с одной виртуальной машины на другую.
Подключение по внутреннему IP-адресу возможно только с виртуальных машин, которые принадлежат к одной [облачной сети](../../vpc/concepts/network.md#network).

Внутренний IP-адрес не меняется всё время существования виртуальной машины.


## Внешний IP-адрес {#external-ip}

Вы можете присвоить виртуальной машине внешний IP-адрес. По этому адресу виртуальная машина будет доступна в сети Интернет.

Внешний IP-адрес назначается автоматически, выбрать его нельзя. Адрес выделяется из пула адресов Яндекс.Облака.

Во время работы виртуальной машины внешний IP-адрес не меняется. Если виртуальная машина длительное время отключена, то внешний IP-адрес может быть отозван. Тогда при следующем включении виртуальной машины ей будет выделен присвоен новый внешний IP-адрес.

Внешний IP-адрес, назначенный виртуальной машине, сопоставляется ее внутреннему IP-адресу с использованием NAT. Поэтому все запросы к виртуальной машине по внешнему IP-адресу передаются на ее внутренний IP-адрес. Подробнее о NAT читайте в [RFC 3022](https://www.ietf.org/rfc/rfc3022.txt).


## Имя хоста и FQDN {#hostname}

При создании виртуальной машины ей будет присвоено имя хоста и FQDN. FQDN можно использовать для доступа с одной виртуальной машины на другую в рамках одной облачной сети.

Вы можете задать имя хоста при создании. Если имя хоста не указать, то в качестве имени хоста будет использован ID виртуальной машины.

На основании имени хоста будет создано доменное имя хоста (FQDN) в следующем формате:

```
hostname.zone_id.internal
```

Например, если вы указали имя хоста `myinstance` и создали виртуальную машину в зоне доступности `ru-central1-a`, то FQDN будет таким:

```
myinstance.ru-central1-a.internal
```


## MAC-адрес {#mac-address}

После подключения сетевого интерфейса к виртуальной машине, ему будет присвоен MAC-адрес устройства.

Вы можете узнать MAC-адрес в самой виртуальной машине или в информации о ресурсе через API Яндекс.Облака.