# Panic
Protection and notification

PANIC is an open source monitoring and notification system for Cosmos-SDK, Substrate and Chainlink based nodes from Simply VC. The tool was built with user needs in mind and has many features such as phone calls for critical alerts, installation via Web-UI and Telegram/Slack alerts.

 Installing Git
 *Skip if Git is already installed.

   ``bash
   # install git
   sudo apt install git
   
   check
   git --version
   ```
 #### Installing Docker and Docker Compose

 Skip if Docker and Docker Compose is already installed

 ``bash
 # install docker and docker-compose
 curl -sSL https://get.docker.com/ | sh
 sudo apt install docker-compose -y

 check
 docker --version
 docker-compose --version
 ```

 Install configuration

 ``bash
 # clone the repo and go to the
 git clone https://github.com/SimplyVC/panic
 cd panic
 ```

 In the `panic` directory, edit the parameters in the `.env` file

 - INSTALLER_USERNAME: user

 - INSTALLER_PASSWORD: password

 - UI_ACCESS_IP: IP address of the host where PANIC is installed (available scripts/get_ip_linux.sh and scripts/get_ip_mac.sh to determine ip address)

 ``ini
 UI_ACCESS_IP=1.1.1.1
 INSTALLER_USERNAME=panic_user
 INSTALLER_PASSWORD=panic_password
 ```

 Launch Panic

 After configuring all the parameters run Panic with this command:

 ``bash
 docker-compose up -d --build
 ```
 If the build fails, we remove the docker images with the following command, fix the cause of the failure and start the build again:

 ``bash
 docker-compose kill
 docker system prune -a --volumes
 docker-compose up -d --build
 ```

 To make sure that the system is working correctly, you can use the commands `docker-compose logs -f alerter` and `docker-compose logs -f health-checker`.

 The log files are located in the `panic/alerter/logs` directory

 Setting up Telegram notifications

 To create **Telegram bot**, add [@BotFather](https://telegram.me/BotFather) to Telegram, click Start, and perform the following steps:

 1. send a command `/newbot` and give the requested data including bot name and user name

 2. Write down API token, which looks like:`11111111:AAA-AAA11111111-aaaaa11111`.

 3. Click on the link `t.me/<username>` to access the created bot and click `Start`.

 4. Follow the link `api.telegram.org/bot<token>/getUpdates`, replacing the `<token>` received bot token. Opens up a list of bot activity, including the messages sent to him

 5. There should be at least one message in the list, triggered by clicking Start. If not, send the bot the `/start` command. Fix the value of `"id"` in the `"chat"` section.

 6. This completes the creation of the bot, to create another bot, repeat the above steps again

    **As a result we should get

    - Telegram account
    - Telegram bot
    - Telegram bot API token
    - Chat ID (`chat ID`) 

 Configuring monitoring and alerts

 The configuration of node monitoring and notification channels is done at `https://{UI_ACCESS_IP}:8000`. For authorization we use `INSTALLER_USERNAME` and `INSTALLER_PASSWORD` which we specified in file `.env`. 

 After authorization, the monitoring wizard starts. All necessary actions are intuitive and commented in detail.
