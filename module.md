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
    """Docstring for command"""
    args = get_args(message)
    if not args:
        return await message.answer("Команда введа без аргументов")
    else:
        return await message.answer(f"Команда введена с аргументами: <code>{args}</code>")

@validator.command("premium", require_premium=True)
async def command_for_premium_users(bot: Client, message: Message):
    """Docstring for command"""
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
    """Docstring for command"""
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
    """Docstring for command"""
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
    """Docstring for command"""
    if not hasattr(bot.db.<DEV>, "TOKENS"):
        bot.db.<DEV>.new_db("TOKENS")
    
    TOKENS_DB = bot.db.<DEV>.TOKENS
    token = TOKENS_DB.get(str(message.from_user.id))
    await message.answer(f"<b>Ваш токен: <code>{token}</code></b>")

@validator.command("get_all_tokens", only_owners=True)
async def get_all_users_tokens(bot: Client, message: types.Message):
    """Docstring for command"""
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
# Inline SpotifyNow Module
```python
import spotipy
from spotipy.oauth2 import SpotifyOAuth
from pyrogram import types

from ...custom_decorators import inline_query, command
from ...utils import get_args

def get_auth_manager():
    return SpotifyOAuth(
        client_id="dc60d69ab3294f138668d4018bbc4021",
        client_secret="03292c8175c746b28348c668b215e717",
        redirect_uri="http://spotitoken.farkhodovme.tk/",
        scope=(
            "user-read-playback-state playlist-read-private playlist-read-collaborative"
            "app-remote-control user-modify-playback-state user-library-modify"
            "user-library-read"
        )
    )


@command("setSpotifyToken")
async def set_spotify_token(bot, message: types.Message):
    """Docstring for command"""
    token = get_args(message)
    if not token:
        return await message.answer("Пожалуйста введите <b>Spotify-TOKEN</b>.")

    devDB = bot.db.<DEV>
    if not hasattr(devDB, "Spotify"):
        devDB.new_db("Spotify")

    db = devDB.Spotify
    db.set(str(message.from_user.id), token.strip())
    return await message.answer(
        "✅ Ваш <b>Spotify-TOKEN</b> был <b>успешно сохранен</b>!",
        [
            [
                {
                    "text": "Inline-Spotify",
                    "switch_inline_query_current_chat": "spotify",
                }
            ]
        ]
    )


async def get_spotify_now_track(bot, result):
    user_id = result.from_user.id
    db = bot.db.<DEV>.Spotify

    sp = spotipy.Spotify(auth=db.get(f"{user_id}"), auth_manager=get_auth_manager())
    current_track = sp.current_user_playing_track()

    if current_track is None:
        return await result.answer_media(
            types.InputMediaPhoto(
                "https://cdn-icons-png.flaticon.com/512/16/16187.png",
                caption="😵‍💫 | <b>На данный момент не поет ничего.</b>",
            ),
            reply_markup=[
                [
                    {
                        "text": "Inline-Spotify-Now",
                        "switch_inline_query_current_chat": "spotify",
                    }
                ]
            ]
        )

    track_name = current_track["item"]["name"]
    artists = ", ".join([artist["name"] for artist in current_track["item"]["artists"]])
    album = current_track["item"]["album"]["name"]
    release_date = current_track["item"]["album"]["release_date"]
    image_url = current_track["item"]["album"]["images"][0]["url"]

    return await result.answer_media(
        types.InputMediaPhoto(
            image_url,
            (
                f"<b>{track_name} Now playing\n\n"
                f"Artists: {artists}\n"
                f"Album: {album}\n"
                f"Release date: {release_date}</b>"
            )
        )
    )



@inline_query(
    command="spotify",
)
async def inline_spotify(bot, query: types.InlineQuery):
    """Docstring for command"""
    devDB = bot.db.<DEV>
    if not hasattr(devDB, "Spotify"):
        devDB.new_db("Spotify")
    db = devDB.Spotify
    if not db.get(str(query.from_user.id)):
        return await query.answer([
            types.InlineQueryResultArticle(
                title="🚫 Отсутствует Spotify-TOKEN",
                input_message_content=types.InputTextMessageContent(
                    "🚫 У вас <b>отсутствует Spotify-TOKEN</b>!\nℹ️ Чтобы его сохранить, напишите <a href=\"https://t.me/aozoram_bot/\">боту в лс</a> команду: <code>/setSpotifyToken TOKEN</code>",
                ),
                description="ℹ️ Вы не сохранили TOKEN :(",
                thumb_url="https://img.icons8.com/stickers/100/null/behavior-blocker.png", thumb_height=100, thumb_width=100
            )
        ], 10, is_personal=True)

    return await query.answer(
        [
            query.result(
                types.InlineQueryResultPhoto(
                    "https://images.wallpaperscraft.ru/image/single/nadpis_ozhidanie_podsvetka_134404_1280x720.jpg",
                    "https://img.icons8.com/office/80/hourglass-sand-bottom.png",
                    photo_width=1280,
                    photo_height=720,
                    caption="<b>Загружаю информацию о текущем проигрывающемся треке...</b>",
                ),
                get_spotify_now_track,
            )
        ], 10, is_personal=True,
    )
```
> spotifyNowInline.py
<p align="center">
    <a href='https://github.com/Den4ikSuperOstryyPer4ik/Aozora-Docs/blob/main/README.md'>
    <img width="64" height="64" src="https://img.icons8.com/flat-round/64/home--v1.png" alt="home--v1"/>
    <h2 align="center">Главная страница</h2>
    </a>
</p>
<a href='https://github.com/Den4ikSuperOstryyPer4ik/Aozora-Docs/blob/main/README.md'>
    <img src="https://te.legra.ph/file/42f3f93f3a0492c1fdccf.png" alt="Aozora">
</a>