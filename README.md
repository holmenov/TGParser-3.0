# Инструкция TGParser

## Возможности парсера
- Сбор всех каналов из 47 тематик на сайте [TGSTAT](https://tgstat.ru/).
- Фильтрация каналов по открытым комменатариям.
- Фильтрация каналов по дате выхода последнего поста.
- Фильтрация каналов по минимальному количеству охватов.
- Проверка в отфильтрованных каналах наличия анти-спам бота.
- Использование прокси
- Добавлять/удалять каналы-исключения, которые не нужно парсить.
- Возобновление работы в случае IP-адреса TGSTAT'ом на этапе парсинга каналов.
- Возобновление работы в случае блокировки аккаунта ТГ на этапе проверки анти-спам бота.

## Внешний вид парсера

![](https://i.imgur.com/rJgWwVi.png)

## Инструкция по установке
Перед использованием бота необходимо скачать [Python](https://www.python.org/ftp/python/3.11.1/python-3.11.1-amd64.exe). Во время установки не забудьте установить галочку напротив "Add python.exe to PATH".

![Установка Python](https://i.imgur.com/9Vdl03a.png)

После того как мы установили Python, заходим в папку с парсером, в которой мы запускаем файл "TGParser.exe", ожидаем полной установки необходимых библиотек.

![Копирование ключа](https://i.imgur.com/juiKFrN.png)

Как только у нас появится интерфейс с надписью "Ваше устройство не авторизовано...", вам нужно будет нажать на кнопку "Скопировать" и отправить его разработчику в ЛС, чтобы добавить ваше устройство в базу.

Также перед использованием парсера вам нужно скачать Google Chrome и обновить его до последней версии. Сделать это можно здесь: **chrome://settings/help** (Вставьте это в адресную строку Google Chrome).

## Инструкция по парсеру

Перед началом использования парсера, необходимо в папку *session* закинуть файл сессии (аккаунт). Сессия **обязательно** должна быть формата telethon, название сессии может быть любое.

После того, как мы закинули аккаунт можно открывать парсер и переходить к настройкам самого парсера.

![Внешний вид парсера](https://i.imgur.com/cTizfgD.png)

Взаимодействовать с парсером можно с помощью кнопок, которые находятся в левой части приложения, попозже мы разберем каждое из них.

## Настройка парсера

Для того, чтобы настроить парсер нужно выбрать пункт настройки, при нажатии которого у нас откроется меню с настройками парсера. Давайте пройдемся по каждому пункту:

![](https://i.imgur.com/652HSj5.png)

- **Исключать пройденные ранее каналы** - Этот переключатель отвечает за автоматическое добавление каналов в каналы-исключения. Т.е когда вы запустите парсер с этим параметром и бот начнет проходит каналы, он будет их автоматически добавлять в каналы-исключения и при следующем парсинге бот не будет взаимодействовать с этими каналами. Также если вы захотите, то можете почистить список с каналами-исключениями, чтобы они не пропускались при парсинге.

- **Использовать прокси** - Этот переключатель отвечает за использование прокси, TGSTAT любит блокировать IP-адреса при больших кол-вах запросов к сайту. Поэтому если жалко свой IP или парсите за раз слишком много каналов 500+, то обязательно используем прокси.

- **Ссылка в Telegram** - В этом поле нам необходимо указать ссылку, которая будет отправляться в комментарии для проверки на анти-спам бота. Если ссылка удалится, то значит анти-спам бот есть и такой канал пропустится, если же бота нету, то ссылка не удалится.

- **Тематика** - Выбираем тематику, которую хотим пропарсить.

- **Кол-во каналов для парсинга** - Здесь вписываем количество каналов, которое мы хотим пропарсить.

- **Минимальное кол-во охватов** - Вписываем минимальное кол-во охватов для каналов, которые мы хотим получить.

- **Ожидание для анти-спам бота (сек.)** - Указываем через сколько секунд парсер будет проверять наличие отправленного комментария в каналах. Некоторые анти-спам боты удаляют комментарии не сразу, а через 3-10 сек. Ставим подходящее для вас число.

- **Макс. кол-во каналов для остановки** - В данном параметре мы задаем лимит "плохих" каналов для перехода парсера к следующему этапу. Например возьмем цифру 20, т.е если мы поставили парситься 3000 каналов и парсер находит 20 каналов подряд, которые не попадают под условия (меньше мин. кол-во охватов, либо закрыты комментарии), он переходит к следующему этапу (К проверке каналов в ТГ на анти-спам бота).

- **Дата самого свежего поста** - Вписываем сюда дату последнего поста в формате (ДД:ММ:ГГГГ), от которой хотим искать каналы. Т.е если мы впишем сюда 11.04.2023 и если попадется канал, в котором пост вышел 10.04.2023 и ранее, то этот канал пропуститься. Если же последний пост вышел 11.04.2023 и позднее, то канал не пропустится.

- **Данные прокси** - Вписываем данные прокси в формате "ip:port@login:password". Поддерживаются прокси формата IPv4 HTTP(S).

Как только мы вписали все необходимые настройки для парсера, нажимаем кнопку сохранить, чтобы сохранить внесенные изменения.

## Остальные пункты в меню

### Проверка каналов

В этом пункте мы можем добавить наши каналы которые, например, мы нашли в ручную несколько недель назад и хотим проверить их на наличие анти-спам бота, т.к админы могли за это время поставить анти-спам бота от спамеров.

![](https://i.imgur.com/O4EdM5k.png)

Для этого просто вносим в поле каналы и нажимаем кнопку "Добавить каналы в базу". После запускаем парсер, он сразу перейдет к проверке в Telegram.

### Исключения

В этом меню мы можем изменить список каналов, которые парсер будет пропускать при парсинге. Если у вас включена функция "Исключать пройденные ранее каналы", то пройденные каналы будут автоматически заноситься в этот список.

![](https://i.imgur.com/IxKhxJi.png)

Здесь вы можете как добавить свои каналы, так и удалить все или какие-то конкретные каналы.

### Результаты

В этом меню мы можем получить результаты парсинга, если вы ранее не парсили каналы, то вы получите надпись "Результаты не найдены...".

Если же парсер завершил работу и уведомил вас в логах о том, что можно получить каналы в меню "Результаты", то мы получим 3 кнопки в этом меню, нажимая по которым можем получить нужные нам каналы.

![](https://i.imgur.com/hBptCLv.png)

- **Скопировать подходящие каналы** - Каналы с открытыми комментариями, без анти-спам ботов
- **Скопировать каналы с закрытым чатом** - Каналы с закрытым чатом, в которые нужно вступить чтобы отправлять комментарии.
- **Скопировать каналы с анти-спам ботом** - Каналы с открытыми комментариями с анти-спам ботом.

### Временные файлы

Здесь мы можем управлять временными файлами, которые содержат в себе каналы Telegram и каналы с TGSTAT. Т.е, если у нас бот закрылся с ошибкой на этапе TGSTAT'a, то создается файл TGSTAT и если бот увидит данный файл при следующем запуске, то продолжит работу с прошлого запуска.

Точно также эта система работает и с этапом Telegram, когда например у нас банят аккаунт, создается временный файл Telegram, который делает авто-сейв каналов, чтобы вы могли потом продолжить работу.

![](https://i.imgur.com/3ECEUmz.png)

Если же вы вдруг захотите начать все сначала, для этого и придумана это меню, здесь вы можете удалить временные файлы и бот начнет все сначала.

### Настройки

По этому пункту мы уже проходили чуть выше, поэтому описывать его еще раз нету смысла.

### Ключ

В данной меню ничего особенного нету, здесь мы просто можем скопировать ключ нашего устройства.

![](https://i.imgur.com/Zdg2idg.png)

## Запуск софта

После того, как мы выставили нужные нам настройки, закинули бота в папку session, можем приступать к работе.

Софт запускается с помощью зеленой кнопки "Запустить". Сначала бот ищет каналы в нужной тематике по TGSTAT'у, далее сортирует каналы по заданным вами параметрам и после чего переходит в Telegram.

В Telegram бот автоматически отправляет комментарии и проверяет каналы на наличие анти-спам бота, который сам удаляет комментарии с ссылками.

### Рабочие нюансы

- Во время работы парсера на этапе проверки анти-спам бота в канале, ваш аккаунт Telegram может забанить или отправить в спам-блок, с которого идет проверка. **Поэтому не используйте свои личные аккаунты!**
- В парсере нереализована функция паузы во время работы, т.е если вы во время работы нажмете кнопку "Остановить", то бот остановит работу и закроет приложение.
- Не рекомендуется менять аккаунты Telegram прямо во время работы, лучше остановите бота, замените аккаунты и после продолжите работу.
- Если вы захотите воспользоваться функцией "Проверка каналов", то убедитесь что вы не потеряете важные данные во временном файле Telegram, т.к при использовании данной функции этот файл удалится. Если в прошлый запуск парсера, парсинг на этапе Telegram'а завершился с ошибкой, то вы не сможете продолжить работу по сохраненным каналам, после запуска функции "Проверка каналов".