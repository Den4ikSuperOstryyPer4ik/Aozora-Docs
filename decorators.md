<a href='https://t.me/aozoram_bot'>
    <img src="https://te.legra.ph/file/42f3f93f3a0492c1fdccf.png" alt="Aozora">
</a>

# Примеры декораторов для Aozora:


## Декоратор stats
``` python
from ...custom_decorators import validator

@validator.stats(str(dev_user_id)) # декоратор будет собирать статистику модуля 

#ps. вставится под декором command вставьте на команду на которую юзер обязан использовать
```
> Пример использования декоратора stats
``` python
from ...custom_decorators import validator

@validator.command("start")
@validator.stats('742333517')
async def start_command(bot: Client, message: Message):
    ...
```


##  Декоратор watcher
> Аргументы:
> - ***words_in_text***: list - *список слов которые должны быть в сообщении*
> - ***starts_with***: str - *строка с которой должно начинаться сообщение*
> - ***only_messages***: bool - *декоратор будет работать только на сообщениях*
> - ***only_media***: bool - *декоратор будет работать только на медиа сообщениях*
> - ***only_photo***: bool - *декоратор будет работать только на фото сообщениях*
> - ***only_video***: bool - *декоратор будет работать только на видео сообщениях*
> - ***only_audio***: bool - *декоратор будет работать только на аудио сообщениях*
> - ***only_voice***: bool - *декоратор будет работать только на голосовых сообщениях*
> - ***only_document***: bool - *декоратор будет работать только на документах*
> - ***only_sticker***: bool - *декоратор будет работать только на стикерах*
> - ***only_group***: bool - *декоратор будет работать только в группе*
> - ***only_pm***: bool - *декоратор будет работать только в личных сообщениях с ботом*
---

``` python
from ...custom_decorators import validator

@validator.watcher() # декоратор будет работать только на сообщениях

@validator.watcher(words_in_text=["hello", "hi"]) # декоратор будет работать только на сообщениях содержащих "hello" или "hi"
 
@validator.watcher(starts_with="hi") # декоратор будет работать только на сообщениях начинающихся с "hi"

@validator.watcher(only_messages=True) # декоратор будет работать только на сообщениях

@validator.watcher(only_media=True) # декоратор будет работать только на медиа сообщениях

@validator.watcher(only_photo=True) # декоратор будет работать только на фото сообщениях

@validator.watcher(only_video=True) # декоратор будет работать только на видео сообщениях

@validator.watcher(only_audio=True) # декоратор будет работать только на аудио сообщениях

@validator.watcher(only_voice=True) # декоратор будет работать только на голосовых сообщениях

@validator.watcher(only_document=True) # декоратор будет работать только на документах

@validator.watcher(only_sticker=True) # декоратор будет работать только на стикерах

@validator.watcher(only_group=True) # декоратор будет работать только в группе

@validator.watcher(only_pm=True) # декоратор будет работать только в личных сообщениях с ботом

```

##  Декоратор command
---

> Аргументы:
> - ***only_allowed***: bool - *команду могут использовать только разрешенные пользователи*
> - ***only_pm***: bool - *команда будет работать только в личных сообщениях с ботом*
> - ***only_group***: bool - *команда будет работать только в группе*
> - ***only_group_admins***: bool - *команда будет работать только администраторам и владельцу группы*
> - ***only_premium***: bool - *команда будет работать только у Premium-юзеров TG*
> - ***require_args***: bool - *декоратор проверит указаны ли аргументы после команды*
> - ***require_reply***: bool - *декоратор проверит есть ли реплей*

---
``` python
from ...custom_decorators import validator

@validator.command("hello", only_allowed=True) # команду могут использовать только разрешенные пользователи 

@validator.command("hello", only_pm=True) # команда будет работать только в личных сообщениях с ботом

@validator.command("hello", only_group=True) # команда будет работать только в группе

@validator.command("hello", only_group_admins=True) # команда будет работать только администраторам и владельцу группы

@validator.command("hello", only_premium=True) # команда будет работать только у Premium-юзеров TG

@validator.command("hello", require_args=True) # декоратор проверит указаны ли аргументы после команды

@validator.command("hello", require_reply=True) # декоратор проверит есть ли реплей 

```


##  Декоратор callback_query
---
> Аргументы:
> - ***only_allowed***: bool - инлайн кнопка будет работать только у разершенных пользователей
> - ***only_premium***: bool - инлайн кнопка будет работать только у премиум пользователей телеграм
> - ***only_group_admins***: bool - инлайн кнопка будет работать только у администраторов и владельца группы
---
``` python
from ...custom_decorators import validator

@validator.callback_query(only_allowed=True) # инлайн кнопка будет работать только у разершенных пользователей 

@validator.callback_query(only_premium=True) # инлайн кнопка будет работать только у премиум пользователей телеграм

@validator.callback_query(only_group_admins=True) # инлайн кнопка будет работать только у администраторов и владельца группы
```
---
<p align="center">
    <a href='https://github.com/Den4ikSuperOstryyPer4ik/Aozora-Docs/blob/main/README.md'>
    <img width="64" height="64" src="https://img.icons8.com/flat-round/64/home--v1.png" alt="home--v1"/>
    <h2 align="center">Главная страница</h2>
    </a>
</p>