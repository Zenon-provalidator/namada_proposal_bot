# Namada Proposal Bot

## How to install

### Clone the Github URL

Clone `https://github.com/Zenon-provalidator/namada_proposal_bot` in the `/go/src/github.com/` folder

### Make binary
Do `go build` in the `/go/src/github.com/namada_proposal_bot` folder

### Create Service File
Create a `namada_proposal_bot.service` file in the `/etc/systemd/system` folder with the following code snippet. Make sure to replace USER with your Linux user name. You need sudo previlege to do this step.
```
[Unit]
Description=namada_proposal_bot daemon
After=network-online.target

[Service]
User=$USER
ExecStart=$HOME/go/src/github.com/namada_proposal_bot/namada_proposal_bot
WorkingDirectory=$HOME/go/src/github.com/namada_proposal_bot/
Environment=DAEMON_NAME=namada_proposal_bot
Environment=DAEMON_HOME=$HOME/go/src/github.com/namada_proposal_bot
Environment=DAEMON_LOG_BUFFER_SIZE=512

Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
```

### Enable Service
sudo systemctl enable namada_proposal_bot.service

### Config
Change to `local1.yaml.exam` to `prod.yaml` in the `/go/src/github.com/namada_proposal_bot/config` folder and Save the config fit for you.

### Start Service
sudo systemctl start namada_proposal_bot.service

### Check logs
sudo journalctl -fu namada_proposal_bot.service

## DataBase

### Table Create
```
CREATE TABLE `proposals` (
  `id` int NOT NULL AUTO_INCREMENT,
  `chain_name` varchar(45) NOT NULL,
  `proposal_id` varchar(45) NOT NULL,
  `type` varchar(128) DEFAULT NULL,
  `title` varchar(200) NOT NULL,
  `description` varchar(15000) NOT NULL,
  `status` varchar(45) NOT NULL,
  `submit_time` datetime NOT NULL,
  `deposit_end_time` datetime NOT NULL,
  `voting_start_time` datetime NOT NULL,
  `voting_end_time` datetime NOT NULL,
  `update_date` datetime DEFAULT CURRENT_TIMESTAMP,
  `msg_id` int NOT NULL,
  `is_alert` tinyint DEFAULT '0',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=1 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```
