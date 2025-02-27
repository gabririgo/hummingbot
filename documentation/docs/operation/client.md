# The Hummingbot Client

Hummingbot uses a command-line interface (CLI) that helps users configure and run the bot, as well as generate logs of the trades performed.

## Starting Hummingbot

### Installed from Docker

Creating a new instance of Hummingbot with `docker run` will automatically start the Hummingbot client (see Docker installation guides for [Windows](/installation/windows), [Linux](/installation/linux) and [MacOS](/installation/macOS)).

To run a previously created, stopped container where $NAME is the name of your instance of Hummingbot:

```sh
docker start $NAME && docker attach $NAME
```

For additional information on useful commands, see the [cheatsheet](/cheatsheets/docker) to running Hummingbot on Docker.

### Installed from Source

!!! note
    Make sure that you activate the Anaconda environment with `conda activate hummingbot` prior to running Hummingbot.

Open a Terminal window and go to the root of the directory that contains Hummingbot. From there, run:
```
bin/hummingbot.py
```

### Trading Strategy Autostart

Hummingbot can automatically start the execution of a previously configured trading strategy upon launch without requiring the Hummingbot interface `config` and `start` commands.  Any parameters that are required for `config` can be passed into the Hummingbot launch command.

**Launch command**

```bash tab="Docker command"
docker run -it \
-e STRATEGY=${STRATEGY} \
-e CONFIG_FILE_PATH="/hummingbot_files/hummingbot_conf/${CONFIG_FILENAME}" \
--name hummingbot-instance \
--mount "type=bind,source=$(pwd)/hummingbot_files/hummingbot_conf,destination=/conf/" \
--mount "type=bind,source=$(pwd)/hummingbot_files/hummingbot_conf,destination=/logs/" \
coinalpha/hummingbot:latest
```

```bash tab="Installed from source"
bin/hummingbot_quickstart.py \
--strategy ${STRATEGY} \
--config-file-path "conf/${CONFIG_FILENAME}" \
--wallet ${WALLET} \
--wallet_password ${WALLET_PASSWORD}
```

## User Interface

### Client Layout
![Hummingbot CLI](/assets/img/hummingbot-cli.png)

The CLI is divided into three panes:

* **Input pane (lower left)**: where users enter commands
* **Output pane (upper left)**: prints the output of the user's commands
* **Log pane (right)**: log messages


| Command | Function |
|---------|----------|
| `help` | Prints a list of available commands.
| `start` | Starts the bot. If any configuration settings are missing, it will automatically prompt you for them.
| `config` | Configures or, if a bot is already running, re-configures the bot.
| `status` | Get a status report about the current bot status.
| `list` | List wallets, exchanges, configs, and completed trades.<br/><br/>*Example usage: `list [wallets|exchanges|configs|trades]`*
| `get_balance` | Get the balance of an exchange or wallet, or get the balance of a specific currency in an exchange or wallet.<br/><br/>*Example usage: `get_balance [-c WETH -w|-c ETH -e binance]` to show available WETH balance in the Ethereum wallet and ETH balance in Binance, respectively*.
| `exit`| Cancels all orders, saves the log, and exits Hummingbot.
|`exit -f`| Force quit without cancelling orders.
| `stop` | Cancels all outstanding orders and stops the bot.
|`export_private_key`| Print your ethereum wallet private key.
|`history`| Print bot's past trades and performance analytics. For an explanation of how Hummingbot calculates profitability, see our blog [here](https://hummingbot.io/blog/2019-07-measure-performance-crypto-trading/#tldr).
|`export_trades`| Export your trades to a csv file.

## Bounty-Related Commands

| Command | Description |
|-------- | ----------- |
| `bounty --register` | Register to participate in for liquidity bounties.
| `bounty --list` | See a list of active bounties.
| `bounty --restore-id` | If you lost your configuration file, this is the command to restore it.
| `bounty --status` | See your accumulated rewards.
| `bounty --terms` | See the terms & conditions.

## Keyboard shortcuts
| Keyboard Combo | Command | Description |
|-------- | ----------- | ----------- |
| `Double CTRL + C` | Exit | Press `CTRL + C` twice to exit the bot.
| `CTRL + S` | Status | Show bot status.
| `CTRL + F` | *Search / Hide Search | Toggle search in log pane.
| `CTRL + A` | Select All | Select all text in input pane [used for text edit in Input pane only].
| `CTRL + Z` | Undo | Undo action in input pane [used for text edit in Input pane only].
| `Single CTRL + C` | Copy | Copy text [used for text edit in Input pane only].
| `CTRL + V` | Paste | Paste text [used for text edit in Input pane only].

***Note about search:***

1. Press `CTRL + F` to trigger display the search field

2. Enter your search keyword (not case sensitive)

3. Hit `Enter` to jump to the next matching keyword (incremental search)

4. When you are done. Press `CTRL + F` again to go back to reset.
