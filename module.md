<a href='https://t.me/aozoram_bot'>
    <img src="https://te.legra.ph/file/42f3f93f3a0492c1fdccf.png" alt="Aozora">
</a>

# Примеры модулей для Aozora:
## Quick start:
``` python
from pyrogram.client import Client
from pyrogram import types

from ...custom_decorators import validator
from ...utils.msg import get_args

@validator.command("test")
async def test_command(bot: Client, message: Message):
    args = get_args(message)
    if not args:
        return await message.answer("Команда введа без аргументов")
    else:
        return await message.answer(f"Команда введена с аргументами: <code>{args}</code>")

@validator.command("premium", require_premium=True)
async def command_for_premium_users(bot: Client, message: Message):
    return await message.answer("Спасибо, Premium-пользователь, что воспользовался командой!")
```
>  quickstart.py
---
## Web2File Module:
``` python
from pyrogram.client import Client
from pyrogram import types

from ...custom_decorators import validator
from ...utils.msg import get_args

import io, requests

@validator.command("web2file", require_arg=True)
async def web2file(bot: Client, message: types.Message):
    link = get_args(message)
    try:
        file = io.BytesIO(requests.get(link).content)
    except Exception:
        return await message.answer("🚫 <b>Ошибка загрузки</b>")
    
    file.name = link.split("/")[-1]

    return await message.answer_media(file, caption="<b>Загруженный файл:</b>")
```
> web2file.py
---
# Tokens module
```python
from pyrogram.client import Client
from pyrogram import types

from ...custom_decorators import validator
from ...utils.msg import get_args

@validator.command("set_token", require_arg=True)
async def set_user_token(bot: Client, message: types.Message):
    token = get_args(message)
    if not hasattr(bot.db.<DEV>, "TOKENS"):
        bot.db.<DEV>.new_db("TOKENS")
    
    TOKENS_DB = bot.db.<DEV>.TOKENS
    TOKENS_DB.set(
        str(message.from_user.id),
        token
    )
    await message.answer("<b>Ваш токен успешно сохранен!</b>")

@validator.command("get_token")
async def get_user_token(bot: Client, message: types.Message):
    if not hasattr(bot.db.<DEV>, "TOKENS"):
        bot.db.<DEV>.new_db("TOKENS")
    
    TOKENS_DB = bot.db.<DEV>.TOKENS
    token = TOKENS_DB.get(str(message.from_user.id))
    await message.answer(f"<b>Ваш токен: <code>{token}</code></b>")

@validator.command("get_all_tokens", only_owners=True)
async def get_all_users_tokens(bot: Client, message: types.Message):
    if not hasattr(bot.db.<DEV>, "TOKENS"):
        bot.db.<DEV>.new_db("TOKENS")
    
    tokens = []
    TOKENS_DB = bot.db.<DEV>.TOKENS
    for user_id, token in TOKENS_DB.items():
        tokens += [f"<code>{user_id}</code>: <code>{token}</code>"]
    
    await message.answer("<b>Все токены в БД:</b>\n" + "\n".join(tokens))
```
> tokens_example.py
---
<p align="center">
    <a href='https://github.com/Den4ikSuperOstryyPer4ik/Aozora-Docs/blob/main/README.md'>
    <img width="64" height="64" src="https://img.icons8.com/flat-round/64/home--v1.png" alt="home--v1"/>
    <h2 align="center">Главная страница</h2>
    </a>
</p>
<a href='https://github.com/Den4ikSuperOstryyPer4ik/Aozora-Docs/blob/main/README.md'>
    <img src="https://te.legra.ph/file/42f3f93f3a0492c1fdccf.png" alt="Aozora">
</a>