# Видео
[![Настройка сервера для Foundry VTT на Android: Пошаговое руководство](https://i.ytimg.com/vi/fXraqq5lp-4/hqdefault.jpg?sqp=-oaymwEcCPYBEIoBSFXyq4qpAw4IARUAAIhCGAFwAcABBg==&rs=AOn4CLDNdjYppQGSGLENIe2XGjkCryaMvQ)](https://youtu.be/fXraqq5lp-4)

## Требуемые технические характеристики к серверу

**Минимальные:**
* 1 vCPU
* Место на диске: 1GB
* 2 GB RAM
* Firewall и настройки безопасности настроены так, что позволяют игрокам зайти на сервер на необходимый порт.

**Рекомендуемые:**
* 2 vCPU
* Место на диске: 1GB
* 4 GB RAM
* Firewall и настройки безопасности настроены так, что позволяют игрокам зайти на сервер на необходимый порт.

_Объем памяти, требуемый серверным процессом, зависит от объема данных, включенных в игровую систему и модулей, которые активны в вашем мире. Для более крупных систем или миров, в которых используются более ресурсоемкие модули, потребуется больше оперативной памяти._

**Рекомендую сервера AEZA, сам ими пользуюсь. По этой [реферальной ссылке](https://aeza.net/?ref=352255) вы получите +15% к пополнению в первые 24 часа.**

## Установка Foundry VTT на Android

Друзья, добрый день! Это инструкция, как запустить foundry на вашем смартфоне/планшете.

### Установка и настройка Termux

1. Для начала нам нужно установить [Termux](https://github.com/termux/termux-app/releases) на ваше устройство
2. Введите команду `termux-wake-lock`, у вас должно высветиться окошко или открыться настройки. Необходимо дать возможность приложению не выгружаться из памяти.
3. Введите следующие команды:
   1. `pkg update`
   2. `pkg upgrade`
   
   ***При выполнении этих команд нажимайте все время Enter***
4. Установите **OpenSSH**
   1. `pkg install openssh`
5. Установите **Node.js**
   1. `pkg install nodejs`
6. Установите **wget**
   1. `pkg install wget`
7. Введите следующую комманду:
   1. `cd $HOME`
9. Создайте 2 папки, используя следующие комманды:
   1. `mkdir foundryvtt`
   2. `mkdir foundrydata`
10. Перейдите на [FoundryVTT](https://foundryvtt.com/). После авторизации необходимо получить ссылку на архив с файлами Foundry в **Purchased Licenses**, выбрать Linux/NodeJS, нажать **TIMED URL**

![FOUNDRY](/misc/images/img1.png "San Juan Mountains")

11. Введите следующие комманды:
    1. `cd foundryvtt`
    2. `wget -O foundryvtt.zip 'ССЫЛКА, которую скопировали в предыдущем шаге'`
    (ссылка должна быть в кавычках)
    3. `unzip foundryvtt.zip`
   
12. Запустите Foundry:
    1. `node $HOME/foundryvtt/resources/app/main.js --dataPath=$HOME/foundrydata`

### Дополнительные настройки

#### В Termux 
1. Ввести команду `passwd`, необходимо ввести пароль и еще раз его повторить
2. Запустить `sshd`

#### В PowerShell (Windows)
1. Ввести `Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'`
2. Ввести `ssh -p '8022' '192.168.1.4'`, где **192.168.1.4** это **ip** вашего телефона/планшета, узнать можно например [здесь](https://www.whatismybrowser.com/detect/what-is-my-local-ip-address) 
3. Теперь вы можете подключаться к своему серверу на телефоне/планшете из терминала на компьюетере.

## Полезные ссылки

1. [How to Install Foundry on an Android Phone](https://foundryvtt.wiki/en/setup/hosting/Installing-on-Android)
2. [Get started with OpenSSH for Windows](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=powershell)
3. [Remote Access (Termux SSH)](https://wiki.termux.com/wiki/Remote_Access#SSH)