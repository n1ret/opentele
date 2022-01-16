<!-- vim: syntax=Markdown -->

# OpenTele
A python library created to make life easier for Telegram API Developers.

## Main Features
- Convert [Telegram Desktop](https://github.com/telegramdesktop/tdesktop) **tdata** sessions to [telethon](https://github.com/LonamiWebs/Telethon) sessions and vice versa.
- Use [telethon](https://github.com/LonamiWebs/Telethon) with [official APIs](#authorization) to avoid unnecessary problems.
- Randomize `device info` using real data that recognized by Telegram server.

## Dependencies

- [telethon](https://github.com/LonamiWebs/Telethon) - Widely used Telegram's API library for Python.
- [tgcrypto](https://github.com/pyrogram/tgcrypto) - AES-256-IGE encryption to works with `tdata`.
- [pyQt5](https://www.riverbankcomputing.com/software/pyqt/) - Used by Telegram Desktop to streams data from files.

## Installation
- Install from [PyPI](https://pypi.org/project/opentele/):
```pip title="pip"
pip install --upgrade opentele
```

## First Run
- Load TDesktop from tdata folder and convert it to telethon, with a custom API.
```python
from opentele.td import TDesktop
from opentele.td import APITemplate
from opentele.tl import TelegramClient
from opentele.utils import CreateNewSession, UseCurrentSession

async def main():
    
    # Load TDesktop client from tdata folder
    tdataFolder = "Path\\To\\tdata"
    tdesktop = TDesktop(tdataFolder)

    # Using official iOS API with randomly generated device info
    # print(api) to see more
    api = APITemplate.TelegramIOS.Generate()

    # Convert TDesktop session to telethon client
    # CreateNewSession flag will use the current existing session to
    # authorize the new client by `Login via QR code`.
    client = await tdesktop.ToTelethon("newSession.session", CreateNewSession, api)

    # Although Telegram Desktop doesn't let you authorize other
    # sessions on desktop client (or doesn't have that feature),
    # it is still available for all platforms (APIs).

    # Connect and print all logged in devices
    await client.connect()
    await client.PrintSessions()

asyncio.run(main())
```

## Authorization
OpenTele offers the ability to use the **official APIs**, which are used by official apps. You can check that out [here](https://github.com/thedemons/opentele/blob/main/docs/content/api-documentation/authorization/apitemplate#telegramdesktop-objects).
<br>
According to [Telegram TOS](https://core.telegram.org/api/obtaining_api_id#using-the-api-id): all accounts that sign up or log in using unofficial Telegram API clients are automatically put under observation to avoid violations of the Terms of Service.
<br>
<br>
It also uses the **official [lang_pack](https://core.telegram.org/method/initConnection)** parameter, of which [telethon can't use](https://github.com/LonamiWebs/Telethon/blob/master/telethon/client/telegrambaseclient.py#L375) because it's only for official apps.
<br>
Therefore, **there are no differences** between using OpenTele and official apps, the server can't tell you apart.

## Incoming Features
- [x] Writing data to tdata for converting telethon sessions to tdesktop
- [x] Random device information for [initConnection](https://core.telegram.org/method/initConnection) to perform mass registeration without being detected
- [ ] Add supports for [pyrogram](https://github.com/pyrogram/pyrogram)

## Documentation
- [ ] Half way done

## License

The subscription fee is one ⭐ per month.
.. just kidding

