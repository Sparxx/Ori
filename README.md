
# Ori

Scrapers for multiple platforms integrated into popular solana bots

Written in golang






## Features

- Telegram scraping
- Discord scraping



## Documentation

#### Download:

Head over to [releases](https://github.com/Sparxx/Ori/releases/new) to download the latest version for your os


#### TOML Config:
    [General]

    buy_once - bot will only attempt to snipe a ca once. Any time the ca is sent 
    again it will not attempt to buy

    variable_market - for pumpfun urls only. Attempts to determine the proper 
    market being pumpfun/ray - Requires Solana RPC

    auto_update - set to true to automatically download and run the latest version

    blacklisted_words - blacklisted words to block when filtering. e.g 'hi\b' is blacklisted means any message with hi in it should not be scraped - SEE REGEX SECTION

    port - port which quicktask is hosted on

    markets - markets to attempt to snipe for token address, e.g raydium, orca, meteora


    [Telegram]

    tg_api - The app ID for the telegram app you create

    tg_hash - The hash id for the telegram app you create

    client_ids - ID's from the accounts you want to monitor - forward any msg to @getidsbot

    channel_ids - ID's from the channels you want to monitor - forward any msg to @getidsbot - remove -100

    group_ids - ID's from a groupchat you want to monitor - use @raw_data_bot but remove - before the number

    phone_number - # linked to the tg account used for monitoring - include country code (1 for USA)

    strict_casing - will only scrape messages when group_id and client_id match

    scrape_dms - if true will only scrape tg dms - ignores groupchats


    [Discord]

    token - the discord token of the account you are using to scrape

    user_ids - The user ID's of accounts to monitor for all messages sent

    channel_ids - The channel ID's of channels to monitor all messages sent

    server_ids - The server id of channels to monitor all messages sent

    strict_casing - if true will only scrape if user id and channel id match - ignores server id


    [solana]

    rpc - Solana rpc http url used for requests

    retries - the amount of retries for solana requests made 


#### Telegram Setup:

 Go [here](https://my.telegram.org/apps) to create a Telegram app, then get your app ID and hash ID 

![image](https://github.com/user-attachments/assets/2de3023a-4d3d-4261-9974-263ce9d1a879)

Once you have your app ID and hash ID, make sure your phone number is correct and with the correct country code. The Bot will prompt you for a code upon starting the scraper that you will get from a Telegram DM

Once logged in, the bot saves your login as a session file in the sessions folder

In order to login with a different account, move or delete the session.dat file and it will recreate one with the new app id + hash + number


#### Discord Setup:

Follow [this](https://www.androidauthority.com/get-discord-token-3149920/) if you don't know how to get your discord token 

In order to get channel, server and user ID's, enable developer mode under Advanced in settings

![image](https://github.com/user-attachments/assets/fa97ed08-8d27-463e-bef5-6b85d8ecd401)

The bot can monitor as many users/channel ID's as you want but keep in mind on discord's end there are rate limits

To scrape dms or groupchats, get the channel ID from them

**RISK - Using user tokens to scrape can lead to a ban as it is against Discord TOS**


#### Filters:

Filters are pretty modular in the sense that you can do a lot with them and are the same across discord and tg.

If all fields are empty, the bot will attempt to scrape everything

if one or more filter fields are filled and some remain empty, messages pertaining to the empty field will not be scraped

e.g I have server ID filled with user ID - only the users messages in that server will be scraped, in any channel

e.g I have channel ID filled with no user ID, any message in that channel from anyone will be scraped

e.g I have strict casing enabled and channel ID + user ID set. Only messages from that user in the set channel will be scraped

e.g I have user ID and channel ID filled without strict casing, any message sent in that channel will be scraped, and any message sent
by the user even in other discords will be scraped - if you add server ID it will limit it to only those servers


#### Blacklist:

Blacklist uses golang regex format

you can go [here](https://regex101.com/) to test your regex 

in blacklisted words, you do not have to input (i?) or chain your words with "|", its automatically done

format example is ['\bword1\b', 'word2', 'word3']

You also have the freedom to metacharacters to your words for better filtering












