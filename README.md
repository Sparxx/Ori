
# Ori

Scrapers for multiple platforms integrated into popular solana bots






## Features

- Telegram
- Discord



## Documentation

#### TOML Config:
    [General]

    buy_once - bot will only attempt to snipe a ca once. Any time the ca is sent 
    again it will not attempt to buy

    variable_market - for pumpfun urls only. Attempts to determine the proper 
    market being pumpfun/ray - Requires Solana RPC

    port - port which quicktask is hosted on

    markets - markets to attempt to snipe for token address, e.g raydium, orca, meteora


    [Telegram]

    tg_api - The app ID for the telegram app you create

    tg_hash - The hash id for the telegram app you create

    client_ids - ID's from the accounts you want to monitor - forward any msg to @getidsbot

    channel_ids - ID's from the channels you want to monitor - forward any msg to @getidsbot

    phone_number - # linked to the tg account used for monitoring - include country code (1 for USA)


    [Discord]

    token - the discord token of the account you are using to scrape

    user_ids - The user ID's of accounts to monitor for all messages sent

    channel_ids - The channel ID's of channels to monitor all messages sent


    [solana]

    rpc - Solana rpc http url used for requests

    retries - the amount of retries for solana requests made 


#### Telegram Setup:

 Go [here](https://my.telegram.org/apps) to create a Telegram app, then get your app ID and hash ID 




 ![myimage-alt-tag](https://media.discordapp.net/attachments/293554319767371786/1276813181070868480/rltg.png?ex=66cae470&is=66c992f0&hm=2b2dc271beba8afb5c836fbe93e08c04b5c7a95f7221bd94e92e7ba58858574b&=&format=webp&quality=lossless)


Once you have your app ID and hash ID, make sure your phone number is correct and with the correct country code. The Bot will prompt you for a code upon starting the scraper that you will get from a Telegram DM

Once logged in, the bot saves your login as a session file in the sessions folder

In order to login with a different account, move or delete the session.dat file and it will recreate one with the new app id + hash + number


#### Discord Setup:

Follow [this](https://www.androidauthority.com/get-discord-token-3149920/) if you don't know how to get your discord token 

In order to get channel and user ID's, enable developer mode under Advanced in settings

![myimage-alt-tag](https://media.discordapp.net/attachments/293554319767371786/1276815266512371764/image.png?ex=66cae661&is=66c994e1&hm=e567cd98f193826b9247fa3bb737b525db5e477576bb66874f8eed60d883c0a5&=&format=webp&quality=lossless)

The bot can monitor as many users/channel ID's as you want but keep in mind on discord's end there are rate limits

**RISK - Using user tokens to scrape can lead to a ban as it is against Discord TOS**














