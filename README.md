### Part 1 - Registration

1. Login to [Discord Developer Portal](https://discord.com/developers/applications) or register if you somehow don't have an account.

2. Click `New Application`, go to `Bot` -> Add Bot (keep default settings) -> click `Copy` to copy your token. This token is basically a password, so don't share it with anyone. If you leak it then generate another one. 

3. Go to `OAuth2` -> Add `bot` in scopes -> Add bot permissions (it depends on you bot's purposes, but `send messages`, `read message history`, `mention everyone`, `add reactions`, and `view channels` are basically a must have).

4. Copy the link from the `scopes` field. This is the invitation link that allows you to join the bot to your servers. After using the link (paste it into a web browser) your bot should join a selected server, but it will be offline.

### Part 2 - Code

6. Go to [replit.com](https://replit.com) and create new python repl. Name of the repl is not important. If you want to work on your own server then simply create `main.py` file that you will have to run. 

7. Paste the following code into the `main.py`:

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
# repl (left panel) -> tools -> secrets -> paste the token and name the variable e.g. BOT_TOKEN
client.run(os.getenv('BOT_TOKEN'))

```

8. Run the script. At this point your bot should be online and should reply to the hello message.

### Part 3 - Web server

We need to make our bot to run the web server in order to keep the bot alive (in case of no requests). You can read more  about this issue [here](https://docs.replit.com/hosting/deploying-http-servers).

9. Create file, e.g. `online.py` in your repl and paste this code:

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

10. Update `main.py` by adding  
```python
from online import keep_alive
...
keep_alive()
client.run(os.getenv('BOT_TOKEN'))
```

11. Run the code. A website with white background and text Online should appear. Copy the url of the webpage.

12. Login to [uptimerobot.com](https://uptimerobot.com) (register if needed) and click `Add New Monitor`. Set monitor type to https. Name is not important. Paste your url into the URL field. Set monitoring interval to 5 minutes. Click `Create monitor`.

Your bot is ready and should continue to run, even when there is no activity on your server for a longer peroid of time.
