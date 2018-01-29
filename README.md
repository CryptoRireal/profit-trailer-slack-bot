# Chat Bot for ProfitTrailer

## Installation

### Prerequisites

1. `ruby` must be installed and within your `PATH` scope. If you are unsure what this means, open a command prompt and type `ruby -v`. If you get some similar to `ruby 2.4.2p198 (2017-09-14 revision 59899) [x86_64-darwin16]` you should be golden. If you get an error, head over to [ruby-lang.org](https://www.ruby-lang.org/en/downloads/) and download for your environment.
2. Once you have ruby installed, you will need to install [bundler](http://bundler.io/): `gem install bundler` (this may require `sudo`).

### Slack Setup
1. Go to `http://slack.com/services/new/bot` and login to your workshop. You may need to reload this URL after you intially login.
2. Choose a name for the Slack bot (`profittrailer`) and click "Add bot integration".
3. Copy the "API Token" to be used below.
4. Invite the bot to any room within your workspace that you want with `/invite @profittrailer`.

### Chat Bot Setup
1. Clone this repo to your desired directory. This README and all example values use `/home/pi/PTChatBot` as our installation directory but use whatever location you want.
2. Open a command prompt and `cd` into the chat bot directoyr (`/home/pi/PTChatBot`).
3. Run `bundle install` to install all ruby dependencies.
4. Copy `app.config.example` to `app.config` and open the file in your editor of choice.
5. In `app.config`, update relevant values:
  - `PT_WEB_URL`: If you are running this chat bot on the same machine as ProfitTrailer, you can probably leave this as `localhost`. Otherwise, update for your setup.
  - `PT_WEB_PASSWORD`: Some functionality of this chat bot requires you to have a web password set (you should anyways). You can configure this value within ProfitTrailer in [`application.configuration`](https://wiki.profittrailer.io/doku.php/application.properties) with the `server.password` setting.
  - `PT_LOG_FILE_PATH`: The location of the ProfitTrailer log file. Chat Logger will `tail` this file and parse for Slack messaging.
  - `PT_BOT_BRIDGE`: This is how ChatBot and ChatLogger talk to each other. If this port is in use on your machine, feel free to change it to something else.
  - `PT_LOGGER_SLACK_CHANNEL`: This is the ID of the channel you would like ChatLogger to post logs to. You can find this by going to http://<your-workspace>.slack.com in a web browser. Once you have the web UI open, click on the desired room in the left-hand rooms list and note the ID in the browser address bar: `https://<your-workspace>.slack.com/messages/<this-is-your-channel-id>/`.
  - `PT_LOGGER_SHOW_XXX`: These flags control what and how logs are posted to your Slack channel.

### System Setup (Optional)

If you're on a *nix system, you can use the included service files to control ChatBot and ChatLogger via `systemctl`:
1. Copy the ChatBot service via `sudo cp services/ptchatbot.service.example /etc/systemd/system/ptchatbot.service` and change any relevant paths. You will need to paste the Slack API Token from step 3 above into the `Environment` definition for `SLACK_API_TOKEN`.
2. Copy the ChatLogger service via `sudo cp services/ptchatlogger.service.example /etc/systemd/system/ptchatlogger.service` and change any relevant paths.
3. Update service files to be executable: `sudo chmod u+rwx /etc/systemd/system/chat*.service`.

### Run

1. Open a command prompt and change directories to `/home/pi/PTChatBot`.
2. To run ChatBot, use the `start_bot` command passing in the Slack API Token: `SLACK_API_TOKEN=you-token-here bundle exec ruby start_bot.rb`.
3. To run ChatLogger, use the `start_logger` command: `bundle exec ruby start_logger.rb`. Note that ChatLogger requires that ChatBot is running to work!

## Community

If you have any issues setting up or using these bots, please don't heistate to reach out by creating an Issue here (https://github.com/CryptoRireal/PTChatBot) or finding me on Discord (rireal#2742).

If you found this useful, the best thing you can do is pay it forward. The more we help each other the better we all will be.

If you're feeling generous, the next best thing would be sending tips to a wallet below. This is a perfect way to clear out any dust you may have. :wink: :+1: :100:

BTC: `1BcYAVNvWfLZ6S8jkWMLH8nBN45Wd331aZ`
LTC: `LL9jV5UBVPVGS5GUtGV8SemwZYHGq99ND1`
ETH: `0x4ee33821De66a5A691eA33809695CaDd846d97ab`
BCH: `1BVQm4osGYchAhTMwNW9uTA1eViKmg8otJ`
DASH: `Xn26ncEVp4FtQyBtVBobHrtWcsMjnc3QGy`
