---
title:  "discord.py embed"
excerpt: "embed 설명"

toc: true
toc_sticky: true
toc_label: "페이지 목차"

categories:
  - discord
tags:
  - discord
  - example
  - python
  - embed
last_modified_at: 2020-07-09T17:07:00+09:00
---


## 각종 설명들
```py
embed=discord.Embed(title="Example Embed", description="이것은 Embed입니다.", color=0x00ff56)
```
embed 변수를 만들어 그 안에 Embed 정보를 넣습니다.
title 부분은 제목, description은 설명입니다. 

```py
embed.set_author(name="저자의 이름", url="저자의 URL",, icon_url="저자의 아이콘")
```
저자에 대한 정보를 넣는 구문입니다 (거의 잘 쓰이지는 않습니다)

```py
embed.set_thumbnail(url="아이콘")
```
오른쪽 위에 가장 큰 이미지를 추가하는 코드입니다

```py
embed.add_field(name="필드이름", value="필드값", inline=False)
```
여기서 inline을 True로 하면 가로로 나오게 되고 False로 하면 세로로 나오게 됩니다

```py
embed.set_footer(text="이것은 푸터입니다.")
```
여기부분은 꼬리표인 푸터부분 입니다

## 최종 코드
```py
embed=discord.Embed(title="Example Embed", description="이것은 Embed입니다.", color=0x00ff56)
embed.set_author(name="저자의 이름", url="저자의 URL",, icon_url="저자의 아이콘")
embed.set_thumbnail(url="아이콘")
embed.add_field(name="필드이름", value="필드값", inline=False)
embed.add_field(name="필드이름", value="필드값", inline=False)
embed.add_field(name="필드이름", value="필드값", inline=False)
embed.set_footer(text="이것은 푸터입니다.")
await message.channel.send(embed=embed) #여기는 event용
await ctx.send(embed=embed) #여기는 command용
```