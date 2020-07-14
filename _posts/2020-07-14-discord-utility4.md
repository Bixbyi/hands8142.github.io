---
title:  "discord.py 한명에게 dm 보내기"
excerpt: "한명에게 dm 보내기"

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
last_modified_at: 2020-07-14T14:30:00+09:00
---


## 한명에게 dm 보내기 코드
```py
@client.command(name="DM", pass_context=True)
async def dm(ctx, user: discord.Member, *, content):
    channel = await user.create_dm()
    await channel.send(content)
```

이런식으로 **/DM @유저 안녕** 이런식으로 사용이 가능합니다
create_dm 함수로 편리하게 사용이 가능합니다

## 펄미션 추가하기
```py
@client.command(name="DM", pass_context=True)
@commands.has_permissions(administrator=True)
async def dm(ctx, user: discord.Member, *, content):
    channel = await user.create_dm()
    await channel.send(content)

@dm.error
async def dm_error(ctx, error):
    if isinstance(error, commands.MissingPermissions):
        await ctx.send("{}님, 당신은 이 명령을 실행하실 권한이 없습니다.".format(ctx.message.author))
```