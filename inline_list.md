<a href='https://t.me/aozoram_bot'>
    <img src="https://te.legra.ph/file/42f3f93f3a0492c1fdccf.png" alt="Aozora">
</a>

<br>
<br>
<br>

# <img width="25" height="25" src="https://img.icons8.com/officel/25/info.png" alt="info"/> Метод inline_list:

```python 
...

@validator.command("test")
async def test_command(bot: Client, message: Message):
    """Docstring for command"""
    some_list = ['first', 'second', 'third']
    await bot.inline.list(
        message,
        some_list
    )
```


## Метод использовался в модуле Meaning

```python

# developer: @hikamoru
# description: Urban Dictionary with inline mode
# version: 0.1.0

# lic: This module rewritten from scratch by @hikariatama


import re
import aiohttp
from urllib.parse import quote_plus
from bs4 import BeautifulSoup
from ...custom_decorators import validator, inline_query
from pyrogram import Client
from ...utils import msg
from pyrogram.types import (
    Message,
    InlineQuery,
    InlineQueryResultArticle,
    InputTextMessageContent,
)


HEADERS = {
    "accept": "text/html",
    "user-agent": "Hikka userbot",
}


async def scrape(term: str) -> str:
    term = "".join(
        [
            i.lower()
            for i in term
            if i.lower()
            in "абвгдежзийклмнопрстуфхцчшщъыьэюяabcdefghijklmnopqrstuvwxyz "
        ]
    )
    endpoint = "https://www.urbandictionary.com/define.php?term={}&page={}"
    definitions = []

    async with aiohttp.ClientSession() as session:
        for page in range(1, 4):
            url = endpoint.format(quote_plus(term.lower()), page)
            async with session.request("GET", url, headers=HEADERS) as resp:
                html = await resp.text()

            soup = BeautifulSoup(re.sub(r"<br.*?>", "♠️", html), "html.parser")
            page_definitions = [
                definition.get_text().replace("♠️", "\n")
                for definition in soup.find_all("div", class_="meaning")
            ]
            definitions.extend(page_definitions)

    return definitions


@validator.command("mean", docs="Get the meaning of a word")
async def meaning(client: Client, message: Message):
    mean = await scrape(msg.get_args(message))
    if not mean:
        await message.answer("🤷‍♂️ <b>I don't know what that means</b>", reply=True)
        return
    await client.inline.list(
        message,
        [
            "🧞‍♂️ <b><u>{}</u></b>:\n\n<i>{}</i>".format(msg.get_args(message), mean)
            for mean in mean
        ],
    )


@inline_query(command=["mean", "urban"])
async def inline_mean(client: Client, inline_query: InlineQuery):
    """Get the meaning of a word"""
    args = inline_query.query.replace("mean", "").strip()
    if not args:
        await inline_query.answer(
            results=[],
            switch_pm_text="💬 Please enter a word",
            switch_pm_parameter="start",
        )
        return
    mean = await scrape(args)
    if not mean:
        await inline_query.answer(
            results=[],
            switch_pm_text="🤷‍♂️ I don't know what that means",
            switch_pm_parameter="start",
        )
        return
    await inline_query.answer(
        results=[
            InlineQueryResultArticle(
                title="🧞‍♂️ {}:\n\n{}".format(args, mean),
                description=f"Meaning of {args}",
                input_message_content=InputTextMessageContent(
                    "🧞‍♂️ <b><u>{}</u></b>:\n\n<i>{}</i>".format(args, mean),
                ),
            )
            for mean in mean
        ],
        cache_time=0,
    )


```