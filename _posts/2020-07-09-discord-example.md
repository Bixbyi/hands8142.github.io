---
title:  "discord.py 예제"
excerpt: "event와 command"

toc: true
toc_sticky: true
toc_label: "페이지 목차"

categories:
  - discord
tags:
  - discord
  - example
  - python
last_modified_at: 2020-07-09T08:49:00+09:00
---


## event를 활용한 예제

```py
import discord #모듈

client = discord.Client()


@client.event
async def on_ready():
    print("다음으로 로그인합니다")
    print(client.user.name)
    print(client.user.id)
    print('Discord.py 버전 : ' + discord.__version__)
    print("bot starting..")  # 봇 시작이라고 뜨게하기
    print("==========")
    guilds_count = len(client.guilds)
    members_count = 0

    for guild in client.guilds:
        members_count += len(guild.members)
    print("서버 수: " + str(guilds_count))#서버수 뜨게하기
    print("멤버 수: " + str(members_count))#유저수 뜨게하기
    await client.change_presence(activity=discord.Game("/help"))


@client.event
async def on_message(message):
    if message.content.startswith("/ping"): #/ping 메시지를 받으면 실행
        await message.channel.send("퐁")

    if message.content.startswith("/embed"): #/embed 메시지를 받으면 실행
        embed = discord.Embed(title="타이틀 입니다", colour=discord.Colour.blue())
        embed.set_author(name="한동수가 만듬")
        embed.add_field(name="1", value="11", inline=False)
        embed.add_field(name="2", value="22", inline=False)
        embed.add_field(name="3", value="33", inline=False)
        embed.add_field(name="4", value="44", inline=False)
        await message.channel.send(embed=embed)


client.run("TOKEN")
```


## command를 이용한 예제

```py
import discord #모듈
from discord.ext import commands


client = commands.Bot(command_prefix="/")
client.remove_command('help')


@client.event
async def on_ready():
    print("다음으로 로그인합니다")
    print(client.user.name)
    print(client.user.id)
    print('Discord.py 버전 : ' + discord.__version__)
    print("bot starting..")#봇 시작이라고 뜨게하기
    print("==========")
    guilds_count = len(client.guilds)
    members_count = 0

    for guild in client.guilds:
        members_count += len(guild.members)
    print("서버 수: " + str(guilds_count))#서버수 뜨게하기
    print("멤버 수: " + str(members_count))#유저수 뜨게하기
    await client.change_presence(activity=discord.Game("/help"))

@client.command(name="ping")#/ping 메시지를 받으면 실행
async def ping(ctx):
    await ctx.send("pong")

@client.command(name="embed")#/embed 메시지를 받으면 실행
async def embed(ctx):
    embed = discord.Embed(title="타이틀 입니다", colour=discord.Colour.blue())
    embed.set_author(name="한동수가 만듬")
    embed.add_field(name="1", value="11", inline=False)
    embed.add_field(name="2", value="22", inline=False)
    embed.add_field(name="3", value="33", inline=False)
    embed.add_field(name="4", value="44", inline=False)
    await ctx.send(embed=embed)
                                 
client.run("TOKEN")
```

## 저의 생각

저는 event 보다 command가 좋다고 생각합니다 event도 장점도 많이 있지만 command의 장점이 더 많이 있기 때문이죠
