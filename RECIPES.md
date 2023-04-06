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
