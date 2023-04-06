### Part 1 - Registration

1. Go to [Discord Developer Portal](https://discord.com/developers/applications) and create account for your bot. This is parallel to your personal Discord account, so trying to login in a usual way won't work. 

2. Verify your account and go to the Developer Portal. 

3. Go to `Bot` -> Add Bot (Keep default settings) -> Copy Token. This token is basically a password, so don't share it with anybody. If you leak your token then generate another one. 

4. Go to `OAuth2` -> Add `bot` in scopes -> Add bot permissions (it depends on you bot's purposes, e.g. `send messages`, `read message history`, `mention everyone`, `add reactions`, `view channels`) -> After setting the permissions copy the link from the scopes field. This is an invitation link that allows you to connect the bot to your servers. 

5. After using the link your bot should join one of your servers but it will be offline.

### Part 2 - Coding

6. Go to replit.com and creat new python repl. Name of the repl is not important.

7. Paste the following code to the `main.py` file

```python
import discord
import os

client = discord.Client()

@client.event
async def on_ready():
  print('The bot is ready')

@client.event
async def on_message(message):
  if message.author == client.user:
    return
    
  if messsage.content.startswith('hello'):
    await mesage.channel.send('sup')
    
# When using replit (which is public) one must hide the token by creating so called secret
# repl (left panel) -> tools -> secret -> paste the token and name varaible e.g. BOT_TOKEN
client.run(os.getenv('BOT_TOKEN'))

```

8. Run the script

At this point your bot should be online and should reply to the hello message.

### Part 3 - create web server

We need to make our bot to run the web server in order to keep the bot online (in case of no requests). You can read more [here](https://docs.replit.com/hosting/deploying-http-servers) about it.

9. Create file, e.g. `online.py` in your replt and paste this code

```python
from flask import Flask
from threading import Thread

app = Flask('')

@app.route('/')
def home():
  return "Online"

def run():
  app.run(host = '0.0.0.0', port = 8080)

def keep_alive():
  t = Thread(target = run)
  t.start()
```

10. Update `main.py`

Add 
```python
from online import keep_alive
```
and at the bottom
```python
keep_alive()
client.run(os.getenv('BOT_TOKEN'))
```

11. Run the code. A website with text Online should appear. Cody the link of the webpage.

11. Register to [uptimerobot.com](https://uptimerobot.com) and login

13. Click `Add New Monitor`. Monitor type: https. Name is not important. URL: paste the link. Set monitoring interval to 5 minutes. Create monitor.

At this point your bot should continue to run, even when there is no activity on your server for a long peroid of time.
