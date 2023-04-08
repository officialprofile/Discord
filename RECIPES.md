### Add reaction
```python
@client.event
async def on_message(message):
  if message.content == 'hello':
    await message.add_reaction('\U0001F6F8')
```

### Fake typing
```python
@client.event
async def on_message(message):
  if message.content == 'hello':
    async with message.channel.typing():
    await asyncio.sleep(1)
    await message.channel.send('hi')
```

### Mention author's name

```python
@client.event
async def on_message(message):
  if message.content == 'hello':
    await message.channel.send(f'hi {message.author.name}')
```


### Create global variable

```python
client = discord.Client()
...
client.var1 = 21 # This can be changed
var2 = 37        # This cannot
```

### Change presence

#### Watching
```python
@client.event
async def on_ready():
    await client.change_presence(activity=discord.Activity(
        type=discord.ActivityType.watching, name='movie'))
```
#### Listening
```python
@client.event
async def on_ready():
    await client.change_presence(activity=discord.Activity(
        type=discord.ActivityType.listening, name='song'))
```
#### Game
```python
@client.event
async def on_ready():
    await client.change_presence(activity=discord.Game(name="game"))
```
#### Stream
```python
@client.event
async def on_ready():
    await client.change_presence(activity=discord.Streaming(name="stream", url='https://www.youtube.com/watch?v=VmKin2xhKNk'))
```
Of course, the activity can be changed on the fly by adding the code after
```python
@client.event
async def on_message(message):
```
