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