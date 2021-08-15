# install gitbook

#### УСТАНОВКА GITBOOK <a id="&#x443;&#x441;&#x442;&#x430;&#x43D;&#x43E;&#x432;&#x43A;&#x430;-gitbook"></a>

Устанавливаем таймзону:

```text
sudo dpkg-reconfigure tzdata
```

Обновляем убунту:

```text
sudo apt update && sudo apt upgrade -y
```

Устанавливаем пакеты:

```text
sudo apt install -y curl wget vim git unzip socat bash-completion apt-transport-https build-essential
```

Устанавливаем Node.js:

```text
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt install -y nodejs 
```

Проверяем версии:

```text
node -v && npm -v
# v10.15.1
# 6.4.1
```

Обновим npm

```text
sudo npm install -g npm@latest
```

Проверим версию

```text
npm -v# 6.8.0
```

Далее создаем директорию

```text
sudo mkdir /var/www/gitbook
cd /var/www/gitbook
```

Сразу же сюда клонируем нашу репу из гитлаба, моя будет создана в папке “knowledge\_base”.

Теперь установим гитбук глобально

```text
npm install gitbook-cli -g
```

И установим его в текущую папку

```text
gitbook init
```

Теперь в текущей папке у нас будет создан гитбук и мы его даже сможем запустить. Но пока не будем этого делать, нам нужно его немного настроить.

Создаем файл book.json

```text
vim book.json
```

Со следующим содержимым

```text
{
        "root": "./docs",
        "title": "dpkb",
        "author": "devpew",
        "description": "just my knowledge",
        "plugins": [
                "folding-chapters-2",
                "theme-code",
                "-sharing"
        ],
        "pluginsConfig": {
                "theme-default": {
                        "showLevel": false
                }
        }
}
```

Там мы указали некоторые модули, которые мы будем использовать. Теперь их нужно установить командой:

```text
gitbook install
```

Переместим файлы README.md и SUMMARY.md

```text
mv README.md SUMMARY.md /knowledge_base
```

Практически все готово. Теперь если мы запустим нашу базу знаний то там будет только один файл. И это потому, что до запуска нам нужно сгенерировать файл SUMMARY.

На помощь нам приходит плагин

```text
npm install -g gitbook-summary
```

Теперь запускаем его

```text
book sm g
```

Все. Файл сгенерирован. Теперь можем запускать нашу базу.

