<a href='https://t.me/aozoram_bot'>
    <img src="https://te.legra.ph/file/42f3f93f3a0492c1fdccf.png" alt="Aozora">
</a>

# <img width="25" height="25" src="https://img.icons8.com/officel/25/info.png" alt="info"/> Метод answer:
``` python
async def answer(
    response: Union[str, pyrogram.types.Message],
    reply_markup: Union[
        pyrogram.types.InlineKeyboardMarkup,
        pyrogram.types.ReplyKeyboardMarkup,
        pyrogram.types.ReplyKeyboardRemove
    ],
    send: bool = False,
    reply: bool = False,
    **kwargs
):
    """
    Метод для ответа пользователю сообщением
    
    Можно использовать в:
        CallbackQuery._answer(...)
        Message.answer(...)
        ChosenInlineResult.answer(...)
    
    Параметры:
        response: текст сообщения (чтобы скопировать сообщение, можно его передать)
        reply_markup: Клавиатура с кнопками (будь-то инлайн или ReplyKeyboard)
        send: True, если вы хотите не изменить текущее сообщение, а прислать в чат новое
        reply: True, если надо прислать новое сообщение в ответ на текущее (reply to message)
        **kwargs: дополнительные аргументы для сообщения, например:
            entities=[...], reply_to_message_id=..., disable_notification=True
    """
```
## Примеры использования:
```python
await message.answer(
    response=f"Привет, {message.from_user.mention}!\nЯ - Telegram бот",
    reply_markup=pyrogram.types.InlineKeyboardMarkup(
        [
            [
                InlineKeyboardButton(
                    text="Кнопка 1:1",
                    callback_data="1:1",
                ),
                InlineKeyboardButton(
                    text="Кнопка 1:2",
                    callback_data="1:2"
                )
            ],
            [
                InlineKeyboardButton(
                    text="Кнопка 2:1",
                    callback_data="2:1",
                ),
                InlineKeyboardButton(
                    text="Кнопка 2:2",
                    callback_data="2:2"
                )
            ],
        ]
    ),
    reply=True,
    disable_web_page_preview=True,
)
```
---
```python
async def callback(bot, callback_query, row: int, index: int):
    ...


await message.answer(
    response=f"Привет, {message.from_user.mention}!\nЯ - Telegram бот",
    reply_markup=[
        [
            {
                "text": "Кнопка 1:1",
                "callback": callback,
                "kwargs": {
                    "row": 1,
                    "index": 1,
                }
            },
            {
                "text": "Кнопка 1:2",
                "callback": callback,
                "args": (1,2,),
            },
        ],
        [
            {
                "text": "Кнопка 2:1",
                "callback": callback,
                "kwargs": {
                    "row": 2,
                    "index": 1,
                }
            },
            {
                "text": "Кнопка 2:2",
                "callback": callback,
                "args": (2,2,),
            },
        ]
    ],
    reply=True,
    disable_web_page_preview=True,
)
```
---
```python
await message.answer(
    f"Дарова, {message.from_user.mention('брат')}!",
    reply=True,
)
```
---
```python
await chosen_inline_result.answer(
    "<b>Измененное</b> <i>inline</i>-<u>сообщение</u>.",
    parse_mode=pyrogram.enums.ParseMode.HTML,
)
```


---
<p align="center">
    <a href='https://github.com/Den4ikSuperOstryyPer4ik/Aozora-Docs/blob/main/README.md'>
    <img width="64" height="64" src="https://img.icons8.com/flat-round/64/home--v1.png" alt="home--v1"/>
    <h2 align="center">Главная страница</h2>
    </a>
</p>