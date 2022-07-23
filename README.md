# Bot
A template repository that defines the structure for current and future Python bot projects using `discord.py`. This README can be fully replaced with that of a target bot application using this template.

## Configuration
Two files called `config_bot.py` and `config_launch.py` can be used to provide information required for the bot to run. These files are meant to be stored locally on host machines without being 'added' to a Git repository. However, this suggestion may be ignored for workflows that don't permit it.  


### `config_bot.py`
This file is meant to hold the configuration settings, credentials and API endpoints of the bot application. `"client_id"` and `"token"` are meant to be mandatory, whilst others can be fully up to the implementation. For projects that use hosting solutions based on ephemeral file systems, credentials stored within the `"auth"` dictionary like `"client_id"` and `"token"` can be turned into uppercase environment variables prefixed with `AUTH_` (e.g. `AUTH_CLIENT_ID` and `AUTH_TOKEN`) instead. A similar approach can be used for the credentials within `"db"`, using `DB_`. The `config_bot.py` (excluding credentials and sensitive information) file can then be added to the project's Git repository to preserve it in those cases. As this file is a Python file, those credentials can be loaded into the `CONFIG` dictionary during startup.

When loaded, bot applications should only need to search for the `CONFIG` dictionary.

```py
(CONFIG := {
    "auth": {
        "client_id": 1234567891011121314,
        "token": "....",
        "...": "..."
    },
    "db": {
        "postgresql_address": "postgresql://user:password@host/database",
        "sqlite_db": "../../database.db",
        "...": "..."
    }
})
```

### `config_launch.py`
This file is meant to customize the launching/startup process of the bot application. For the dictionaries within the `"exts"` (extensions) list, the `"name"` and `"package"` keys match the names of the `name` and `package` arguments in the `discord.ext.commands.Bot.load_extension` method and the values are meant to be forwarded to it, during startup. `"variables"` can be used as a way to provide keyword arguments to extensions while they load, if supported. For ease of use, a CLI interface could be provided which allows selectively overriding or excluding options from this file when launching a bot application. Depending on the desired workflow, this file may also be added to the Git repository of a bot project.

When loaded, bot applications should only need to search for the `CONFIG` dictionary.

```py
(CONFIG := {
    "exts": [
        {
            "name": ".exts.local_extension",
            "package": "bot",
            "variables": {
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
            "variables": {
                "c": 1,
                "d": 2
            }
        }
    ]
})
```
