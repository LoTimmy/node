        
![](https://cldup.com/PKpktytKH9.png)

### 安裝 {#installing}

```
shell> npm install pm2 -g # Install latest pm2 version
shell> npm install pm2@latest -g
```

```
                        -------------

   Looking for a complete monitoring and management tool for PM2?
    _                             _        _            _
   | | _____ _   _ _ __ ___   ___| |_ _ __(_) ___ ___  (_) ___
   | |/ / _ \ | | | '_ ` _ \ / _ \ __| '__| |/ __/ __| | |/ _ \
   |   <  __/ |_| | | | | | |  __/ |_| |  | | (__\__ \_| | (_) |
   |_|\_\___|\__, |_| |_| |_|\___|\__|_|  |_|\___|___(_)_|\___/
             |___/

                          Features

                   - Real Time Dashboard
                   - CPU/Memory monitoring
                   - HTTP monitoring
                   - Event notification
                   - Custom value monitoring
                   - Real Time log display

                          Checkout

                   https://keymetrics.io/

                        -------------

[PM2] Spawning PM2 daemon
[PM2] PM2 Successfully daemonized
┌──────────┬────┬──────┬─────┬────────┬─────────┬────────┬────────┬──────────┐
│ App name │ id │ mode │ pid │ status │ restart │ uptime │ memory │ watching │
└──────────┴────┴──────┴─────┴────────┴─────────┴────────┴────────┴──────────┘
 Use `pm2 show <id|name>` to get more details about an app
```

```
# Fork mode
shell> pm2 start app.js
shell> pm2 start app.js --name="api" # Start application and name it "api"
shell> pm2 start app.js --no-daemon

# Cluster mode
shell> pm2 start app.js -i 0         # Enable load-balancer and cluster features
shell> pm2 start app.js -i 0         # Will start maximum processes with LB depending on available CPUs

shell> pm2 start app.js --watch      # Restart application on file change

shell> pm2 restart api         
shell> pm2 stop api
shell> pm2 stop 0                    # Stop specific process id

shell> pm2 stop all                  # Stop all apps
shell> pm2 restart all               # Restart all processes

shell> pm2 reload all                # Will 0s downtime reload (for NETWORKED apps)

shell> pm2 delete 0                  # Will remove process from pm2 list
shell> pm2 delete all                # Will remove all processes from pm2 list
```

```
apps:
  - script   : app.js
    instances: 4
    exec_mode: cluster
  - script : worker.js
    watch  : true
    env    :
      NODE_ENV: development
    env_production:
      NODE_ENV: production
```

```
pm2 start process.yml
```

```
apps:
  script    : api.js
  instances : max
  exec_mode : cluster
```

---

![](https://github.com/unitech/pm2/raw/master/pres/pm2-list.png)

```
shell> pm2 list               # List all processes started with PM2
```

```
$HOME/.pm2 will contain all PM2 related files
$HOME/.pm2/logs will contain all applications logs
$HOME/.pm2/pids will contain all applications pids
$HOME/.pm2/pm2.log PM2 logs
$HOME/.pm2/pm2.pid PM2 pid
$HOME/.pm2/rpc.sock Socket file for remote commands
$HOME/.pm2/pub.sock Socket file for publishable events
$HOME/.pm2/conf.js PM2 Configuration
```

```
shell> pm2 generate                  # Generate a sample json configuration file
```

```
# Logs
shell> pm2 logs                      # Display logs of all apps
shell> pm2 reloadLogs                # Reload all logs
shell> pm2 flush                     # Clear all the logs
```

```
shell> pm2 ping                      # Ensure pm2 daemon has been launched
{ msg: 'pong' }
```

---

Monitor all processes

![](http://pm2.keymetrics.io/images/pm2-monit.png)
```
shell> pm2 monit                     # Display memory and cpu usage of each app
```

cluster_mode

---

$HOME/.pm2 will contain all PM2 related files
$HOME/.pm2/logs will contain all applications logs
$HOME/.pm2/pids will contain all applications pids
$HOME/.pm2/pm2.log PM2 logs
$HOME/.pm2/pm2.pid PM2 pid
$HOME/.pm2/rpc.sock Socket file for remote commands
$HOME/.pm2/pub.sock Socket file for publishable events
$HOME/.pm2/conf.js PM2 Configuration

---
#### :books: 參考網站：

- [pm2](https://www.npmjs.com/package/pm2)
- [pm2](http://pm2.keymetrics.io/)
- [quick-start](http://pm2.keymetrics.io/docs/usage/quick-start/)