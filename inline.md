<a href='https://t.me/aozoram_bot'>
    <img src="https://te.legra.ph/file/42f3f93f3a0492c1fdccf.png" alt="Aozora">
</a>

# Inline Docs:

## Декоратор @inline_query():
```python
def inline_query(
    command: str | list[str] = None,
    query: str | list[str] = None,
    query_startswith: str | list[str] = None,
    query_lower: bool = True,
    from_user_id: int | list[int] = None,
    from_user_username: str | list[str] = None,
    chat_type: enums.ChatType | list[enums.ChatType] = None,
    re_match: str | list[str] | dict[str, str] = None,
    for_owners: bool = False,
    for_allowed: bool = False,
):
    """
    Охх, расширный однако декоратор

    Q - InlineQuery.query - хуета какая-та, в общем все после: @username_bot ...

    Параметры:
        command (str | list:str): команда, т.е. первый аргумент, мол:
            @username_bot cmd
            где cmd - команда
        query: требуемое Q, например query="..." и сработает для "@username_bot ..."
        query_startswith: требуемое начало Q, например:
            query_startswith="param param:" - сработает на "@username_bot param param: ...
        query_lower:
            False, если вы хотите, чтобы ваши команды были чувствительны к регистру.
            По умолчанию True.
            Примеры: когда True, command="Start" запускает /Start, но не /start.
        from_user_id: TG-ID юзера или юзеров в тг
        from_user_username: TG-Username человека или нескольких людей в тг
        chat_type: Один или несколько нужных типов чата
        re_match: один или несколько matches
        for_owners: сделать доступность только для овнеров(@hikamorumeh, @Den4ikSOP, @toxicuse)
        for_allowed: сделать доступность только для allowed-юзеров, крч для разрабов модулей
    """
```
### Вы же тоже мало что поняли из информации выше? ну крч да, смотрите примеры, с ними лучше))
---
## Примеры использования инлайна:
```python
from pyrogram.client import Client
from pyrogram import types

from ...custom_decorators import inline_query


@inline_query(
    command="test"
)
async def inline_test(bot: Client, query: types.InlineQuery):
    """
    Хендлер, который работает на:
        @username_bot test
        @username_bot test arguments
        @username_bot test afsdfgs fgdgd arg3 arg4
    В общем на команду test
    """
    return await query.answer([
        types.InlineQueryResultArticle(
            title="типа тест команда",
            input_message_content=types.InputTextMessageContent(
                f"ну типо ты ввел:\n@{bot.me.username} test {query.args_raw}\nэта инлайн, братан!",
            ),
            description="молодой чебурек, ты ввел команду test!",
            thumb_url="https://img.icons8.com/color/64/party-baloon.png",
            thumb_height=64,
            thumb_width=64,
        )
    ], is_personal=True)
```
> команда test, работающая везде, у всех и вся
---
```python
from pyrogram.client import Client
from pyrogram import types

from ...custom_decorators import inline_query


@inline_query(
    command="test2",
    for_owners=True,
)
async def inline_test2(bot: Client, query: types.InlineQuery):
    """
    Хендлер, который работает на:
        @username_bot test2
        @username_bot test2 arguments
        @username_bot test2 afsdfgs fgdgd arg3 arg4
    В общем на команду test2, но только у овнеров
    """
    return await query.answer([
        types.InlineQueryResultArticle(
            title="типа тест2 команда для овнеров",
            input_message_content=types.InputTextMessageContent(
                f"братан, ну типо ты ввел:\n@{bot.me.username} test2 {query.args_raw}\nэта инлайн",
            ),
            description="молодой чебурек(овнер), ты ввел команду test2!",
            thumb_url="https://img.icons8.com/color/64/party-baloon.png",
            thumb_height=64,
            thumb_width=64,
        )
    ], is_personal=True)
```
> команда test2, работающая только у овнеров
---
```python
from pyrogram.client import Client
from pyrogram import types, enums

from ...custom_decorators import inline_query


@inline_query(
    command="test3",
    chat_type=enums.ChatType.PRIVATE,
    for_allowed=True,
)
async def inline_test3(bot: Client, query: types.InlineQuery):
    """
    Хендлер, который работает на:
        @username_bot test3
        @username_bot test3 arguments
        @username_bot test3 afsdfgs fgdgd arg3 arg4
    В общем на команду test3, но только у allowed-юзеров (девов модулей)
        и только в приватных чатах (ЛС)
    """
    return await query.answer([
        types.InlineQueryResultArticle(
            title="типа тест6 команда для allowed'ов и для лс",
            input_message_content=types.InputTextMessageContent(
                f"братан, ну типо ты ввел:\n@{bot.me.username} test3 {query.args_raw}\nэта инлайн с фильтром для allowed-юзеров и для ЛС!",
            ),
            description="молодой чебурек(алловед), ты ввел команду test3!",
            thumb_url="https://img.icons8.com/color/64/party-baloon.png",
            thumb_height=64,
            thumb_width=64,
        )
    ], is_personal=True)
```
> команда test3, работающая только у allowed-ов
---
```python
from pyrogram.client import Client
from pyrogram import types

from ...custom_decorators import inline_query


@inline_query(
    query="test4 ура",
)
async def inline_test4(bot: Client, query: types.InlineQuery):
    """
    Хендлер, который работает на:
        @username_bot test4 ура
        @username_bot TesT4 УрА
        пишите хоть капсом, хоть без него, среагирует
        и все, больше ни на что он не реагирует
    И сработает этот инлайн у всех
    """
    return await query.answer([
        types.InlineQueryResultArticle(
            title="типа \"test4 ура\" команда для всех",
            input_message_content=types.InputTextMessageContent(
                f"ура, роблакс, ну типо ты ввел:\n@{bot.me.username} test4 ура\nэта инлайн для всех!",
            ),
            description="УРААА РООООБЛААКС",
            thumb_url="https://img.icons8.com/color/64/party-baloon.png",
            thumb_height=64,
            thumb_width=64,
        )
    ], is_personal=True)
```
> команда test4, работающая только на "@username_bot test4 ура", и работает у всех пользователей в ТГ
---
```python
from pyrogram.client import Client
from pyrogram import types

from ...custom_decorators import inline_query


@inline_query(
    query_startswith="StartTest5",
    query_lower=False,
    from_user_username=[
        "@durov",
        "@Den4ikSOP",
        "@toxicuse",
    ]
)
async def inline_test5(bot: Client, query: types.InlineQuery):
    """
    Хендлер, который работает на:
        @username_bot StartTest5
        @username_bot StartTest5 arguments
        @username_bot StartTest5 afsdfgs fgdgd arg3 arg4
        На starttest5 не сработает, только на StartTest5, важно сохранение заглавных букв!
    В общем на команду StartTest5, и только у пользователей с определенными юзернеймами
    """
    return await query.answer([
        types.InlineQueryResultArticle(
            title="оо, да ты особенный!",
            input_message_content=types.InputTextMessageContent(
                f"Так, смотри, ты умный, не полуфабрикат, ты ввел правильно \"StartTest5\"!\nКрасава, уважаю!",
            ),
            description="ура, ты умный!",
            thumb_url="https://img.icons8.com/color/64/party-baloon.png",
            thumb_height=64,
            thumb_width=64,
        )
    ], is_personal=True)
```
> команда test5, работающая только на StartTest5, ни starttest5, ни Starttest5, только на StartTest5!
> 
> и только у определенных пользователей с одним из usernames, которые указаны в декораторе!
---
```python
from pyrogram.client import Client
from pyrogram import types

from ...custom_decorators import inline_query


@inline_query(
    command="test6",
    from_user_id=[
        5184725450,
        742333517,
        2085438865,
        1484386024,
        79616282,
        6252893154,
    ]
)
async def inline_test6(bot: Client, query: types.InlineQuery):
    """
    Хендлер, который работает на:
        @username_bot test6
        @username_bot test6 arguments
        @username_bot test6 afsdfgs fgdgd arg3 arg4
    В общем на команду test6, но только у юзеров с айдишками в from_user_id
    """
    return await query.answer([
        types.InlineQueryResultArticle(
            title="типа тест6 команда для особено одаренных!",
            input_message_content=types.InputTextMessageContent(
                f"особо одаренный, ты, СТАЛ ОСОБО ОДАРЕННЫМ!!!!\nурааа, роблакс",
            ),
            description="молодой чебурек, ты ввел команду test6!",
            thumb_url="https://img.icons8.com/color/64/party-baloon.png",
            thumb_height=64,
            thumb_width=64,
        )
    ], is_personal=True)
```
> команда test6, работающая только у людей с айди, который указан в from_user_id, и на команду test6
---
```python
from pyrogram.client import Client
from pyrogram import types

from ...custom_decorators import inline_query


@inline_query(
    re_match=r"testT(.[0-9])",
)
async def inline_testTX(bot: Client, query: types.InlineQuery):
    """
    Хендлер, который работает на:
        @username_bot testT1 \\ вместо 1 можно любую цифру от 0 до 9
        @username_bot testT1 arguments
        @username_bot testT1 afsdfgs fgdgd arg3 arg4
    В общем на команду testT(.[0-9]), у всех
    """
    return await query.answer([
        types.InlineQueryResultArticle(
            title="типа тестТ{цифра}, я ничего не курил :>",
            input_message_content=types.InputTextMessageContent(
                f"брат, ты умни!",
            ),
            description="молодой чебурек, ты ввел команду testT{}!".format(query.match.group(1)),
            thumb_url="https://img.icons8.com/color/64/party-baloon.png",
            thumb_height=64,
            thumb_width=64,
        )
    ], is_personal=True)
```
> команда testTX, работающая у всех, где вместо X - можно любую цифру от 0 до 9
---
```python
from pyrogram.client import Client
from pyrogram import types

from ...custom_decorators import inline_query


@inline_query(
    re_match=[
        r"TestX\=(.*[0-9])",
        r"TestY\=(.*[0-9])",
        r"TestZ\=(.*[0-9])",
    ]
)
async def inline_test8(bot: Client, query: types.InlineQuery):
    """
    Хендлер, который работает на:
        @username_bot test2
        @username_bot test2 arguments
        @username_bot test2 afsdfgs fgdgd arg3 arg4
    В общем на команду test2, но только у овнеров
    """
    return await query.answer([
        types.InlineQueryResultArticle(
            title=f"типа Test?={query.match.group(1)} команда",
            input_message_content=types.InputTextMessageContent(
                f"Это инлайн, ты выбрал что-то одно из Z, X, Y.",
            ),
            description=f"молодой чебурек, ты ввел команду Test(Z/Y/X)={query.match.group(1)}!",
            thumb_url="https://img.icons8.com/color/64/party-baloon.png",
            thumb_height=64,
            thumb_width=64,
        )
    ], is_personal=True)
```
> команды:
> - TestZ=~
> - TestX=~
> - TestY=~
> 
> Где ~ - это любая цифра от 0 до 9
> 
> Команды работают у всех
---
```python
from pyrogram.client import Client
from pyrogram import types

from ...custom_decorators import inline_query


@inline_query(command="cmd")
async def handler_cmd(bot: Client, query: types.InlineQuery):
    """
    Рассмотрим ситуацию, когда чел ввел: @username_bot cmd arg1 test arg3 full "это тоже аргумент, в кавычках"
    Для удобства, было приделано к query много чего:
    """
    args_list = query.args # ["arg1", "test", "arg3", "full", "это тоже аргумент, в кавычках"]
    args_raw = query.args_raw # arg1 test arg3 full это тоже аргумент, в кавычках
    match = query.match # даст что-то, только если в декораторе вы указали аргумент re_match в декораторе
```
> вроде все

# Вроде как многое смог объяснить, дальше сами, или ждите доки по ChosenInlineResult!!
>## P.S. мне дико лень чет делать, поэтому хз когда эти доки по результу выйдут, но если хорошо попросите, то мб мб...
---
<p align="center">
    <a href='https://github.com/Den4ikSuperOstryyPer4ik/Aozora-Docs/blob/main/README.md'>
        <img width="64" height="64" src="https://img.icons8.com/flat-round/64/home--v1.png" alt="home--v1"/>
        <h2 align="center">Главная страница</h2>
    </a>
</p>