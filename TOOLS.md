# TOOLS.md - Local Notes

Skills define *how* tools work. This file is for *your* specifics — the stuff that's unique to your setup.

## 浏览器操作

复杂的浏览器操作可以交给 Claude Code 来运行，我只需要编写提示词即可。不用自己一步步操控。

## 语音转文字

用 Groq API 转写语音（OpenAI key 失效了），命令：
```bash
curl -s https://api.groq.com/openai/v1/audio/transcriptions \
  -H "Authorization: Bearer $GROQ_API_KEY" \
  -H "Content-Type: multipart/form-data" \
  -F file="@/path/to/audio.ogg" \
  -F model="whisper-large-v3" \
  -F language="zh"
```

## 文字转语音 (TTS)

用 Fish Audio API 生成语音（默认 tts 工具不可用），命令：
```bash
curl -s -X POST "https://api.fish.audio/v1/tts" \
  -H "Authorization: Bearer $FISH_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "要说的话",
    "reference_id": "'$FISH_VOICE_ID'"
  }' --output /tmp/fish_voice.mp3
```

**注意：Telegram语音条需要ogg opus格式！** 用ffmpeg转换：
```bash
ffmpeg -y -i /tmp/fish_voice.mp3 -c:a libopus /tmp/fish_voice.ogg
```

然后用 message 工具发送：
```
message action=send channel=telegram target=<chatId> filePath=/tmp/fish_voice.ogg asVoice=true
```

## 表情包 - 坡坡popo

聊天时可以发送坡坡表情包增加趣味！存放位置：`/root/clawd/stickers/popo/`
- popo1.jpg ~ popo8.jpg（8张萌猫表情）

发送方式：
```
message action=send channel=telegram target=<chatId> filePath=/root/clawd/stickers/popo/popo1.jpg
```

使用场景：开心、卖萌、撒娇、打招呼等轻松时刻，不要滥用

## Telegram Chat IDs
- 李同学 (李遁一): `8076803572`

## What Goes Here

Things like:
- Camera names and locations
- SSH hosts and aliases  
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras
- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH
- home-server → 192.168.1.100, user: admin

### TTS
- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is your cheat sheet.
