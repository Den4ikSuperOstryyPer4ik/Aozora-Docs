<a href='https://t.me/aozoram_bot'>
    <img src="https://te.legra.ph/file/42f3f93f3a0492c1fdccf.png" alt="Aozora">
</a>

# <img width="25" height="25" src="https://img.icons8.com/officel/25/info.png" alt="info"/> Метод CallbackQuery.edit:
```python
async def edit(
    text: str,
    parse_mode: Optional["pyrogram.enums.ParseMode"] = None,
    entities: Optional[List["pyrogram.types.MessageEntity"]] = None,
    disable_web_page_preview: Optional[bool] = None,
    reply_markup = Union[
        pyrogram.types.InlineKeyboardMarkup,
        pyrogram.types.ReplyKeyboardMarkup,
        pyrogram.types.ReplyKeyboardRemove
    ],
):
    """
    Метод редактирования сообщения в CallbackQuery!

    Параметры:
        text: новый текст сообщения
        parse_mode: Мод для парсинга текста(text) (enums.ParseMode)
        entities: Энтити для текста(text) (list[types.MessageEntity])
        disable_web_page_preview: True, чтобы убрать превьюшку для ссылок в тексте
        reply_markup: новая клавиатура с кнопками (будь-то инлайн или ReplyKeyboard)
    
    P.S. параметр entities бесполезен, если сообщение в CallbackQuery инлайн и имеет inline_message_id
    """
```
## Примеры использования:
```python
await callback_query.edit(
    f"<i>Вы нажали на<i> <b>кнопку</b>, <b>callback_data которой</b>: <code>{str(callback_query.data)}</code>",
    parse_mode=pyrogram.enums.ParseMode.HTML
)
```
```python
# хендлер для кнопки, только для админов чата (и владельца)
from ...custom_decorators import validator

@validator.callback_query(only_admins=True)
async def user(
    bot: pyrogram.client.Client,
    call: pyrogram.types.CallbackQuery,
    user_id: int,
    action: str,
):
    ... # other code

await callback_query.edit(
    f"А вот {callback_query.from_user.mention('он')}, нажал на кнопку!!!!",
    reply_markup=[
        [
            {
                "text": "Заблокировать безмозглово дауна",
                "callback": user,
                "kwargs": {
                    "user_id": callback_query.from_user.id,
                    "action": "ban",
                }
            }
        ],
        [
            {
                "text": "Кикнуть нахуй",
                "callback": user,
                "args": (
                    callback_query.from_user.id,
                    "kick",
                ),
            }
        ],
        [
            {
                "text": "Замутить!",
                "callback": user,
                "kwargs": {
                    "action": "mute",
                }
            },
        ],
        [
            {
                "text": "пощадить невинного",
                "callback": user,
                "kwargs": {
                    "action": "delete_message"
                }
            }
        ],
    ]
)
```
```python
await callback_query.edit(
    "Кароч, я изменяю сообщение, в котором была нажата кнопка\nGoogle: https://google.com/\nYandex: https://ya.ru/",
    disable_web_page_preview=True,
)
```
---
<p align="center">
    <a href='https://github.com/Den4ikSuperOstryyPer4ik/Aozora-Docs/blob/main/README.md'>
    <img width="64" height="64" src="https://img.icons8.com/flat-round/64/home--v1.png" alt="home--v1"/>
    <h2 align="center">Главная страница</h2>
    </a>
</p>