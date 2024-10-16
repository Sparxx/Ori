# Ori

Scrapers for multiple platforms integrated into popular solana bots

Written in golang

If you'd like to tip you can send sol to sparx.sol

"*" Indicates private/paid module - if interested dm @sparxlol on discord or twitter


## Features

- Telegram scraping
- Discord scraping
- Ethereum* / Solana support
- Copytrade Scraper Utilities*


## Documentation

#### Download:

Head over to [releases](https://github.com/Sparxx/Ori/releases/) to download the latest version for your os


#### TOML Config:
    [General]

    key - For private / purchased modules. Not needed for discord/telegram scraping on solana

    webhook - discord webhook for copytrade utils. Not used in other modules yet.

    buy_once - bot will only attempt to snipe a ca once. Any time the ca is sent 
    again it will not attempt to buy
    
    variable_market - for pumpfun urls only. Attempts to determine the proper 
    market being pumpfun/ray - Requires Solana RPC
    
    auto_update - set to true to automatically download and run the latest version
    
    blacklisted_words - blacklisted words to block when filtering. e.g 'hi' is blacklisted means any message with hi in it should not be scraped - SEE REGEX SECTION

    whitelisted_words - whitelisted words to run, same as blacklisted in format. Whitelisted meaning only messages with x word will be scraped. blacklist overrides whitelist.

    blacklisted_tokens - a text file (tokens.txt or any name) that contains a list of token addresses. The bot updates live with anything you add while it's running

    retries - retries for ALL requests. This includes solana + non solana http requests
    
    port - port which quicktask is hosted on
    
    markets - markets to attempt to snipe for token address, e.g ['raydium', 'meteora', 'pumpfun'] - Blood will only work with these 3 markets currently.

    task_filepath - currently ONLY FOR BLOOD - filepath to task file for migrations

    start_task_on_migration - true/false - will start the specified task file and replace ca with the one detected if token is migrating - must have variable_market true
    

    [Telegram]

    tg_api - The app ID for the telegram app you create

    tg_hash - The hash id for the telegram app you create

    client_ids - ID's from the accounts you want to monitor - forward any msg to @getidsbot

    channel_ids - ID's from the channels you want to monitor - forward any msg to @getidsbot - remove -100

    group_ids - ID's from a groupchat you want to monitor - use @raw_data_bot but remove - before the number

    topic_ids - ID's from a groupchat that is divided into topics. use 0 as the ID for the #general topic channel. To get other topic ID's you can create an invite link and its the last number in the url

    phone_number - # linked to the tg account used for monitoring - include country code (1 for USA)

    strict_casing - will only scrape messages when group_id and client_id match - if scraping topics, it will only scrape when topic_id, group_id, and client_id all match

    scrape_dms - if true will scrape tg dms - uses only client_ids


    [Discord]

    token - the discord token of the account you are using to scrape

    user_ids - The user ID's of accounts to monitor for all messages sent

    channel_ids - The channel ID's of channels to monitor all messages sent

    server_ids - The server id of channels to monitor all messages sent

    strict_casing - if true will only scrape if user id and channel id match - ignores server id

    scrape_dms - enables scraping of dms - useful to reduce http load if you don't want to use proxies

    scrape_embeds - enables scraping of webhooks/embeds - useful to reduce http load if you don't want to use proxies


    [solana]

    rpc - Solana rpc http url used for requests - MUST BE PRESENT NOW FOR BOT TO WORK

    ws - solana websocket url


#### Telegram Setup:

 Go [here](https://my.telegram.org/apps) to create a Telegram app, then get your app ID and hash ID 

![image](https://github.com/user-attachments/assets/2de3023a-4d3d-4261-9974-263ce9d1a879)

Once you have your app ID and hash ID, make sure your phone number is correct and with the correct country code. The Bot will prompt you for a code upon starting the scraper that you will get from a Telegram DM

Once logged in, the bot saves your login as a session file in the sessions folder

You can use different session files in different config setups, but make sure to rename them when genning multiple or they will just be overwritten

In order to login with a different account, move or rename the session.dat file and it will recreate one with the new app id + hash + number

**TOPICS** 

To scrape topics you can get the topic id from the last number in an invite link to that specific topic. To scrape the #General channel - use 0 as the topic_id

#### Discord Setup:

Follow [this](https://www.androidauthority.com/get-discord-token-3149920/) if you don't know how to get your discord token 

In order to get channel, server and user ID's, enable developer mode under Advanced in settings

![image](https://github.com/user-attachments/assets/fa97ed08-8d27-463e-bef5-6b85d8ecd401)

The bot can monitor as many users/channel ID's as you want but keep in mind on discord's end there are rate limits

To scrape dms or groupchats, get the channel ID from them

**IMPORTANT - If there is a lot of http error spam - mainly due to scraping webhooks, dms, message edits, and more all at once, try using proxies**

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


#### Blacklist & Whitelist:

uses golang regex format

you can go [here](https://regex101.com/) to test your regex 

in blacklisted words, you do not have to input (i?) or chain your words with "|", its automatically done

same applies to whitelisted words

format example is ['word1', 'word2', 'word3']

You also have the freedom to add metacharacters to your words for better filtering


#### Proxies:

In proxies folder, create any text file - can be named whatever - and put IP:PORT or IP:PORT:USER:PASS proxies - Can use SOCKS5 for some modules

For telegram, both HTTP and SOCKS5 are supported - Some http proxies may not work - SOCKS5 worked every time extremely well in testing

Use HTTP for everything else including copytrade utility scrapers 


#### Eth Scrapers*: 

Eth scrapers will scrape ethereum token addresses with the same filters and setup as the sol modules. Ori will send the token to maestro or bananagun so make sure you have them set up to just receive a token address and run


#### Copytrade Utils*:

**IMPORTANT**:

All scrapers allow the selection of a text file of tokens/wallets from misc folder or you can copy/paste a list or single token in

For large lists, it is recommended to use proxies. ISP's work very well since all sites have low cloudflare. Residential proxies work but for very large lists they struggle, not ideal

For small lists of tokens you can run local on normal scraper modules - For pumpfun top traders proxies are highly recommended since rate limits are high

**MODULES**:

Pumpfun top traders  - All trade stats for pumpfun coins pre-bonding 

Top Traders - Scrapes top traders for a coin(s)

Wallet Stats - Fetches stats for a wallet(s) including winrate, buys, sells, pnl, etc..

*All data is exported into a csv and put in misc folder*
