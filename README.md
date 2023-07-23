# SageLogger: Python Logger Package

SageLogger is a versatile Python logger package that allows you to create loggers with both remote and local capabilities. The core module, "SageFactory.py," facilitates the creation of loggers with options for SageRemoteLogger (remote) and SageLogger (local). When using SageLogger, you have the flexibility to choose from 7 predefined log types for local logging: DEFAULT, POSITIVE, ONHOLD, NEGATIVE, FROZEN, INFORMATION, and MILD_EXCEPTION. Additionally, you can easily create custom log types to suit your specific needs using the `SageLogger.DynamicType` class.

## Features

### Local Logging Options
SageLogger offers 7 built-in log types for local logging:

1. DEFAULT: The default log type.
2. POSITIVE: For positive events and actions.
3. ONHOLD: To indicate events that are on hold or waiting for further action.
4. NEGATIVE: For negative events or errors.
5. FROZEN: To represent frozen states or events.
6. INFORMATION: For general information logging.
7. MILD_EXCEPTION: To log minor exceptions or errors.
8. DEBUG: To debug and troubleshoot code (disabled by default).
9. AMONGUS: For funny ones. You need to enable it first.

### Custom Local Log Types
Apart from the predefined log types, you can create custom log types using the `SageLogger.DynamicType.fromChar` method or the `SageLogger.DynamicType.fromColoredChar` method for colored logs.

### Remote Logging
SageLogger enables remote logging capabilities through the SageRemoteLogger class. You can load custom APIs for remote logging, and it also provides built-in support for Discord webhook integration.

## Example Code

To create a local logger with SageLogger, you can use the following code:

```python
from SageLogger import SageFactory, Logger

import colorama

sagelogs = SageFactory.create("tester", True)
sagelogs.toggle_type(sagelogs.Type.DEBUG)

sagelogs.log("Checking all types")

for x in sagelogs.Type.__iter__():
    sagelogs.log("Hello World! It's " + x.name, type=x)

sagelogs.log("It's dynamic!", type=Logger.DynamicType.fromChar(sagelogs, "XD"))

sagelogs.log("Doing the test again but with changed borders")

sagelogs.customization.set_border_style(colorama.Fore.GREEN, "()")

for x in sagelogs.Type.__iter__():
    sagelogs.log("Hello World! It's " + x.name, type=x)

sagelogs.log("Disabling some types...")
sagelogs.disable_type(sagelogs.Type.__iter__()[3])
sagelogs.toggle_type(sagelogs.Type.__iter__()[5])
sagelogs.enable_type(sagelogs.Type.DEBUG)

for x in sagelogs.Type.__iter__():
    sagelogs.log("Hello World! It's " + x.name + " - check with above ones! There will be some missing :(", type=x)

sagelogs.log("It's dynamic!", type=Logger.DynamicType.fromColoredChar(sagelogs, colorama.Fore.LIGHTYELLOW_EX, "X"))

sagelogs.log("I'm ID 21", type=Logger.DynamicType.fromColoredChar(sagelogs, colorama.Fore.LIGHTYELLOW_EX, "N"), id=20)

sagelogs.log("I have time", type=Logger.DynamicType.fromColoredChar(sagelogs, colorama.Fore.LIGHTYELLOW_EX, "N"), date=True)
sagelogs.log("I have date", type=Logger.DynamicType.fromColoredChar(sagelogs, colorama.Fore.LIGHTYELLOW_EX, "N"), time=True)
sagelogs.log("I have time and date", type=Logger.DynamicType.fromColoredChar(sagelogs, colorama.Fore.LIGHTYELLOW_EX, "N"), time=True, date=True)
sagelogs.log("I have time and date", type=Logger.DynamicType.fromColoredChar(sagelogs, colorama.Fore.LIGHTYELLOW_EX, "N"), time=True, date=True, timecolor=colorama.Fore.YELLOW, datecolor=colorama.Fore.RED)

sageremotelog = SageFactory.create_discord_webhook_remote("<webhook>", savetofile=True)

sagelogs.log("It's debug", type=sagelogs.Type.DEBUG)
sagelogs.log("Sent to discord", type=sagelogs.Type.INFORMATION)
sageremotelog.log("I sent to discord!")
```

IntelliSense should show you around!

Big issue:
In logs it writes color codes.