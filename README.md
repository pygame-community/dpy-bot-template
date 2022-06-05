# Bot
A template repository that defines the structure for current and future Python bot projects using `discord.py`. This README can be fully replaced with that of a target bot project using this template.

## Configuration files
Two more files called `bot-config.json` and `startup-config.json` can be used to provide information required for the bot to run.


### `bot-config.json`
This file is meant to hold the configuration settings, credentials and API endpoints of the bot application. `bot_id` and `bot_token` are meant to be mandatory, whilst others can be fully up to the implementation.
```json
{
    "bot_id": 1234567891011121314,
    "bot_token": "....",
    "postgresql_address": "postgresql://user:password@host/database",
    "sqlite_db": ".../database.db"
}
```

### `startup-config.json`
This is an example for the structure of the file. `"name"` and `"package"` match the names of the `name` and `package` arguments in the `discord.ext.commands.Bot.load_extension` method. `"options"` can be used as a way to provide arguments to extensions while they load.
```json
{
    "mode": "debug",
    "exts": [
        {
            "name": ".exts.local_extension",
            "package" "bot",
            "options": {
                "a": 1,
                "b": 2
            }
        },
        {
            "name": ".exts.local_extension2",
            "package" "bot"
        },
        {
            "name": "global_extension",
            "options": {
                "c": 1,
                "d": 2
            }
        }
    ]
}
```
