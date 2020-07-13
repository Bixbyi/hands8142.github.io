---
title:  "discord.py 청소기능 넣기"
excerpt: "청소 넣기"

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
last_modified_at: 2020-07-12T01:12:00+09:00
---


## 청소기능 코드
```py
@client.command(name="청소", pass_context=True)
async def _clear(ctx, *, amount=99):
    amount = int(amount)
    if amount >= 100 or amount<= 0:
        await ctx.send("1개부터 99개가지만 해주세요.")
    else:
        await ctx.channel.purge(limit=number + 1)
        await ctx.send("{}개를 삭제하였습니다.".format(number))
```
이렇게 사용하실 수 있습니다 100개 이상으로 하면 렉이 걸리거나 정상적으로 처리가 불가능하니 if로 막았습니다.
그리고 숫자를 적지 않았을 경우 99개로 작동합니다.

## 펄미션을 추가하기
```py
@client.command(name="청소", pass_context=True)
@commands.has_permissions(administrator=True)
async def _clear(ctx, *, amount=99):
    amount = int(amount)
    if amount >= 100 or amount<= 0:
        await ctx.send("1개부터 99개가지만 해주세요.")
    else:
        await ctx.channel.purge(limit=number + 1)
        await ctx.send("{}개를 삭제하였습니다.".format(number))

@_clear.error
async def _clear_error(ctx, error):
    if isinstance(error, commands.MissingPermissions):
        await ctx.send("{}님, 당신은 이 명령을 실행하실 권한이 없습니다.".format(ctx.message.author))
```