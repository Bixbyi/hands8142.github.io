---
title:  "discord.py permissions 권한 넣기"
excerpt: "permissions 권한 넣기"

toc: true
toc_sticky: true
toc_label: "페이지 목차"

categories:
  - discord
tags:
  - discord
  - example
  - python
  - utility
  - permissions
last_modified_at: 2020-07-12T01:12:00+09:00
---

이강의는 전강의와 이어집니다.

## permissions 활용하기
```py
@commands.has_permissions(administrator=True)
```
이구문을 추가하여 관리자만 할 수 있게 바꾸어 줍니다.
일단 추방명령어에 넣어 보도록 하겠습니다.
```py
@client.command(name="추방", pass_context=True)
@commands.has_permissions(administrator=True)
async def _kick(ctx, *, member: discord.Member):
    await member.kick(reason=reason)
    await ctx.send(str(member)+"을(를) 추방하였습니다.")
```

## 에러 처리하기
저구문을 그냥 쓰게 된다면 에러가 날것이다 우리는 이에러를 처리해야 한다
그러기 위해서는 이구문을 추가해보자

```py
@_kick.error
async def _kick_error(ctx, error):
    if isinstance(error, commands.MissingPermissions):
        await ctx.send("{}님, 당신은 이 명령을 실행하실 권한이 없습니다.".format(ctx.message.author))
```
이런식으로 에러를 처리할수 있다

## 최종 코드
```py
@client.command(name="추방", pass_context=True)
@commands.has_permissions(administrator=True)
async def _kick(ctx, *, member: discord.Member):
    await member.kick(reason=reason)
    await ctx.send(str(member)+"을(를) 추방하였습니다.")

@_kick.error
async def _kick_error(ctx, error):
    if isinstance(error, commands.MissingPermissions):
        await ctx.send("{}님, 당신은 이 명령을 실행하실 권한이 없습니다.".format(ctx.message.author))
```