<a href='https://t.me/aozoram_bot'>
    <img src="https://te.legra.ph/file/42f3f93f3a0492c1fdccf.png" alt="Aozora">
</a>

# Инструкция по использованию БД:
```python
# Любой хендлер, будь то на команду, колбек или же инлайн
async def handler(bot: Client, update):
    """
    Хендлер с использованием Базы Данных
    
    Вместо <DEV> писать свой ник, для каждого дева есть свой класс с БД
    Имеющиеся классы: 
        bot.db.DSOP
        bot.db.hikamorumeh
        bot.db.toxicuse
        bot.db.kamol
        bot.db.whypodg
        bot.db.shyatzd
        bot.db.ASNCT
        bot.db.codwiz
    
    !! ЕСЛИ ВЫ БУДЕТЕ ТРОГАТЬ ЧУЖЫЕ БАЗЫ ДАННЫХ - ПИЗДЫ ДАДИМ,
        ДАЖЕ НЕ ДУМАЙТЕ !!
    Используйте только свой класс и свои бд
    """
    developer_db = bot.db.<DEV>
    
    # создаем базу данных для чего-то, допустим для Waka-токенов:
    developer_db.new_db("WakaTokens")
    # после создания, больше создавать не надо

    # теперь эта бд доступна вот так:
    wakadb = developer_db.WakaTokens

    # теперь вы можете делать с БД что захотите

    # например сохранить токен для кого-то:
    user_id = 742333517
    wakadb.set(str(user_id), "<TOKEN>") # или wakadb[str(user_id)] = "<TOKEN>"

    # или получить токен по user_id
    user_token = wakadb.get(str(user_id)) # или wakadb[str(user_id)]

    # или же сохранить какую-нибудь таблицу со статистикой:
    # без разницы вообще, что хотите
    STATA = {
        "1": "@username1",
        "2": "@username2",
        "3": "@username3",
        ...
    }
    wakadb.set("Stata", STATA) # или wakadb["Stata"] = Stata

    # и потом получить ее, когда надо:
    stata = wakadb.get("Stata") # или wakadb["Stata"]

    # в общем все, со СВОИМИ базами данных можете делать что хотите,
    # ТОЛЬКО ЧУЖИЕ НЕ ТРОГАТЬ!
```
---
<p align="center">
    <a href='https://github.com/Den4ikSuperOstryyPer4ik/Aozora-Docs/blob/main/README.md'>
    <img width="64" height="64" src="https://img.icons8.com/flat-round/64/home--v1.png" alt="home--v1"/>
    <h2 align="center">Главная страница</h2>
    </a>
</p>