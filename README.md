# Bot
A template repository that defines the structure for current and future Python bot projects using `discord.py`. This README can be fully replaced with that of a target bot project using this template.

## Configuration
A file called `bot-config.json` and can be used to provide information required for the bot to run.


### `bot-config.json`
This file is meant to hold the configuration settings, credentials and API endpoints of the bot application, as well as customize runtime behavior. `"client_id"` and `"token"` are meant to be mandatory, whilst others can be fully up to the implementation. For projects that use hosting solutions based on ephemeral file systems, credentials stored within the `"bot"` object like `"client_id"` and `"token"` can be turned into uppercase environment variables prefixed with `BOT_` (e.g. `BOT_CLIENT_ID` and `BOT_TOKEN`). The `bot-config.json` (excluding credentials) file can also be added to the project's git repository to keep it around in those cases. 

```json
{
    "bot": {
        "client_id": 1234567891011121314,
        "token": "...."
    },
    "database": {
        "postgresql_address": "postgresql://user:password@host/database",
        "sqlite_db": ".../database.db",
        "...": "..."
    },

    "launch": {
        "mode": "debug",
        "exts": [
            {
                "name": ".exts.local_extension",
                "package": "bot",
                "options": {
                    "a": 1,
                    "b": 2
                }
            },
            {
                "name": ".exts.local_extension2",
                "package": "bot"
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
}
```
The `"launch"` object is meant to customize the launching/startup process of the bot application. For the objects within the `"exts"` (extensions) array, the `"name"` and `"package"` keys match the names of the `name` and `package` arguments in the `discord.ext.commands.Bot.load_extension` method and the values are meant to be forwarded to it. `"options"` can be used as a way to provide arguments to extensions while they load. For ease of use, a CLI interface could be made which allows for selectively overriding or excluding options from this file while the bot application is starting.
