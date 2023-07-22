<a href='https://t.me/aozoram_bot'>
    <img src="https://te.legra.ph/file/42f3f93f3a0492c1fdccf.png" alt="Aozora">
</a>

<br>
<br>
<br>

# <img width="25" height="25" src="https://img.icons8.com/officel/25/info.png" alt="info"/> Метод answer_animation:

```python
async def answer_animation(
    update: types.Message
    | types.CallbackQuery
    | types.Chat
    | types.User
    | types.ChosenInlineResult
    | int
    | str,
    client,
    animation: str | io.BytesIO | typing.BinaryIO,
    caption: typing.Optional[str] = None,
    reply_markup=None,
    send: bool = False,
    reply: bool = False,
    **kwargs,
):
    """
    Метод для ответа пользователю анимацией
    update: объект, который пришел в хэндлер
    client: объект клиента
    animation: анимация, которую надо отправить
    caption: подпись к анимации
    reply_markup: Клавиатура с кнопками (будь-то инлайн или ReplyKeyboard)
    send: True, если вы хотите не изменить текущее сообщение, а прислать в чат новое
    reply: True, если надо прислать новое сообщение в ответ на текущее (reply to message)
    **kwargs: дополнительные аргументы для сообщения, например:
        duration=..., has_spoiler=True, thumb=...
    """
    """
```

## Пример использования animation:

```python
from ...utils import answer_animation

await answer_animation(
    message,
    client,
    animation="https://media.giphy.com/media/3o7aDcz3uEu9viKHF6/giphy.gif",
    caption="Привет, это анимация!",
    ...
)
```

<br>
<br>
<br>

# <img width="25" height="25" src="https://img.icons8.com/officel/25/info.png" alt="info"/> Метод answer_photo:

```python
async def answer_photo(
    update: types.Message
    | types.CallbackQuery
    | types.Chat
    | types.User
    | types.ChosenInlineResult
    | int
    | str,
    client,
    photo: str | io.BytesIO | typing.BinaryIO,
    caption: typing.Optional[str] = None,
    reply_markup=None,
    send: bool = False,
    reply: bool = False,
    **kwargs,
):

    """
    Метод для ответа пользователю фотографией
    update: объект, который пришел в хэндле
    client: объект клиента
    photo: фотография, которую надо отправить
    caption: подпись к фотографии
    reply_markup: Клавиатура с кнопками (будь-то инлайн или ReplyKeyboard)
    send: True, если вы хотите не изменить текущее сообщение, а прислать в чат новое
    reply: True, если надо прислать новое сообщение в ответ на текущее (reply to message)
    **kwargs: дополнительные аргументы для сообщения
    """
```

## Пример использования photo:

```python
from ...utils import answer_photo

await answer_photo(
    message,
    client,
    photo="link_to_photo",
    caption="Привет, это фотография!",
    ...
)
```

<br>
<br>
<br>

# <img width="25" height="25" src="https://img.icons8.com/officel/25/info.png" alt="info"/> Метод answer_video:

```python

async def answer_video(
    update: types.Message
    | types.CallbackQuery
    | types.Chat
    | types.User
    | types.ChosenInlineResult
    | int
    | str,
    client,
    video: str | io.BytesIO | typing.BinaryIO,
    caption: typing.Optional[str] = None,
    reply_markup=None,
    send: bool = False,
    reply: bool = False,
    **kwargs,
):

"""
Метод для ответа пользователю видео
update: объект, который пришел в хэндлер
client: объект клиента
video: видео, которое надо отправить
caption: подпись к видео
reply_markup: Клавиатура с кнопками (будь-то инлайн или ReplyKeyboard)
send: True, если вы хотите не изменить текущее сообщение, а прислать в чат новое
reply: True, если надо прислать новое сообщение в ответ на текущее (reply to message)
**kwargs: дополнительные аргументы для сообщения
"""
```



---

<p align="center">
    <a href='https://github.com/Den4ikSuperOstryyPer4ik/Aozora-Docs/blob/main/README.md'>
    <img width="64" height="64" src="https://img.icons8.com/flat-round/64/home--v1.png" alt="home--v1"/>
    <h2 align="center">Главная страница</h2>
    </a>
</p>
```
