---
title: "Troubleshooting"
weight: 50
---

These are common issues and fixes as well as useful hints.

- If you get Crypto requirements issues, make sure to upgrade <b>pip</b> to the latest, regardless of the OS you are using.

```shell
# Upgrade to the latest PIP to meet the Crypto requirements (Windows Example)
python3 -m pip install --upgrade pip
```

- If you get a <b>KeyError: 'subscription_id'</b> , it's likely the ACCT_KEY is not exported

```shell
~/SCRIPTS/idem ❯ idem describe azure.compute.virtual_machines                                                                                           idem 15:51:32
[ERROR   ] Error during describe: KeyError: 'subscription_id'
{}
```

- You can view the full error messages by using the <b>--hard-fail</b> flag

```shell
~/SCRIPTS/idem ❯ idem describe azure.compute.virtual_machines --hard-fail
[ERROR ] Error during describe: KeyError: 'subscription_id'
Traceback (most recent call last):
File "/Users/sammcgeown/SCRIPTS/idem/.venv/bin/idem", line 8, in <module>
...snip...
File "/Users/sammcgeown/SCRIPTS/idem/.venv/lib/python3.9/site-packages/dict_tools/data.py", line 183, in __getattr__
return self[k]
KeyError: 'subscription_id'
```

- List the idem versions/plugins

```shell

~/SCRIPTS/idem ❯ pip list | grep idem                                                                                                                   idem 15:58:27
idem               14.0.2
idem-aiohttp       3.0.0
idem-aws           0.12.1  /Users/sammcgeown/SCRIPTS/idem/idem-aws
idem-azure-auto    0.0.2   /Users/sammcgeown/SCRIPTS/idem/idem-azure-auto
idem-gitlab        1.0.0   /Users/sammcgeown/SCRIPTS/idem/idem-gitlab
```

- By default <b>idem.log</b> will be written at your environment home, 
you can change the location and log level with idem command line

```shell
Logging Options:
  --log-datefmt LOG_DATEFMT
                        The date format to display in the logs
  --log-file LOG_FILE   The location of the log file
  --log-fmt-console LOG_FMT_CONSOLE
                        The log formatting used in the console
  --log-fmt-logfile LOG_FMT_LOGFILE
                        The format to be given to log file messages
  --log-handler-options [LOG_HANDLER_OPTIONS [LOG_HANDLER_OPTIONS ...]]
                        kwargs that should be passed to the logging handler
                        used by the log_plugin
  --log-level LOG_LEVEL
                        Set the log level, either quiet, info, warning, or
                        error
  --log-plugin LOG_PLUGIN
                        The logging plugin to use

```

- On macOS, you get the error: <b>"[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed"</b><br>
Python 3.6+ now includes its own private copy of OpenSSL 1.0.2. and is configured with its own private openssl directory for root certificates<br>
As noted in the ReadMe, there is a simple double-clickable or command-line-runnable script ("/Applications/Python 3.6/Install Certificates.command") - replace Python 3.6 with your specific Python version, e.g. 3.9 <br>
Detailed information [issue28150](https://bugs.python.org/issue28150)


