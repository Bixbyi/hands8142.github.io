---
title:  "discord.py kick, ban, unban 활용"
excerpt: "kick, ban, unban"

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
last_modified_at: 2020-07-11T19:11:00+09:00
---


## kick 명령어
```py
@client.command(name="추방", pass_context=True)
async def _kick(ctx, *, member: discord.Member):
    await member.kick(reason=reason)
    await ctx.send(str(member)+"을(를) 추방하였습니다.")
```
member: discord.Member는 @유저 라고 유저를 멘션하면 그 유저의 값을 받아 옵니다.
그리고 받아온 값으로 유저를 추방합니다.

## ban 명령어
```py
@client.command(name="밴", pass_context=True)
async def _ban(ctx, *, member: discord.Member):
    await member.ban()
    await ctx.send(str(member)+"을(를) 밴 하였습니다.")
```
@유저 라고 유저를 멘션하면 그 유저의 값을 받아 와서 밴을 시킵니다.

## unban
```py
@client.command(name="언밴", pass_context=True)
async def _unban(ctx, *, member):
    banned_users = await ctx.guild.bans()
    member_name, member_discriminator = member.split('#')
    for ban_entry in banned_users:
        user = ban_entry.user
        if (user.name, user.discriminator) == (member_name, member_discriminator):
            await ctx.guild.unban(user)
            await ctx.send(f"{user.mention}을(를) 언밴 하였습니다.")
            return
```
밴된 유저 리스트를 가져온 뒤 '#'으로 split합니다. 예를 들어 "이름#태그"를 말합니다.
다음에 반복문을 돌려서 그 리스트의 유저의 아이디와 태그 번호가 같을 경우, 언밴합니다.

## 다음시간 미리보기
다음 시간에는 권한을 가지고 있는 사람만 가능하도록 펄 미션 기능을 다룰 예정입니다.