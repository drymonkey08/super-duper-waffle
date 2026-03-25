# Content Automation Blueprint
## Premeditated Millionaire — Full Pipeline

> Target: <2 hours/week to run all channels post-setup.
> Stack: n8n (self-hosted or cloud) as the orchestration layer.

---

## Pipeline Overview

```
[CONTENT IDEA] → [SCRIPT GEN] → [VOICEOVER] → [VIDEO GEN] → [EDIT/CAP] → [SCHEDULE] → [POST]
   ChatGPT          ChatGPT        ElevenLabs    Runway ML      CapCut       Buffer/Publer   5 Platforms
```

---

## Phase 1: Manual → Hybrid (Months 1–3)

Do this manually first to learn what works. Then automate what repeats.

| Step | Tool | Time/wk (manual) | Time/wk (automated) |
|---|---|---|---|
| Content ideation | ChatGPT | 30 min | 5 min (review) |
| Script writing | ChatGPT | 60 min | 10 min (review) |
| Voiceover | ElevenLabs | 20 min | 2 min (trigger) |
| Video generation | Runway ML | 45 min | 10 min (review) |
| Captions/editing | CapCut | 30 min | 10 min |
| Scheduling/posting | Buffer/Publer | 30 min | 5 min (review queue) |
| **TOTAL** | | **~3.5 hrs** | **~42 min** |

---

## n8n Workflow Architecture

### Workflow 1: Script Generator
```
Trigger: Schedule (Mon/Wed/Fri 8am)
  → ChatGPT Node: Generate 3 scripts per niche (masculinity + satisfying)
  → Google Sheets Node: Save scripts to content calendar
  → Slack/Discord Node: Notify for review
```

**ChatGPT Prompt Template (Masculinity):**
```
You are a social media scriptwriter for a faceless masculinity & luxury content channel.
Write a 45-second voiceover script with:
- A strong hook in the first 5 words
- Tone: stoic, powerful, aspirational — not motivational fluff
- Theme: [INSERT THEME]
- End with a thought-provoking question or statement
- No emojis in the script itself
Output ONLY the script. No commentary.
```

**ChatGPT Prompt Template (Satisfying):**
```
You are a social media caption writer for a satisfying/relaxing AI content channel.
Write 4 caption variations for a video of [INSERT VISUAL DESCRIPTION].
Each caption: 1-2 sentences, no more than 10 words, with a calm/ASMR tone.
Include 10 relevant hashtags per caption.
```

---

### Workflow 2: ElevenLabs Voiceover Generator
```
Trigger: Google Sheets Row Updated (script approved)
  → ElevenLabs API Node: Generate audio from script
    → Voice ID: [Select deep, calm, authoritative male voice]
    → Model: eleven_multilingual_v2
    → Stability: 0.75 | Similarity: 0.85
  → Google Drive Node: Save .mp3 to /voiceovers/[date]/
  → Google Sheets Node: Update status to "VO Ready"
```

**Recommended ElevenLabs Voices:**
- "Adam" — deep, authoritative, works for stoic content
- "Antoni" — smooth, luxury feel
- Custom clone — record 30 min of your own voice for PM brand

---

### Workflow 3: Runway ML Video Queue
```
Trigger: Google Sheets Row Updated (VO Ready)
  → Runway ML API Node: Generate video from prompt
    → Use stored visual prompts from content calendar
    → Duration: 5s or 10s clips per scene
    → Resolution: 1280x720 (upscale in post if needed)
  → Google Drive Node: Save video clips to /raw-clips/[date]/
  → Google Sheets Node: Update status to "Clips Ready"
  → Notify: Discord/Slack for manual edit review
```

**Note:** Runway ML API has rate limits. Batch generate 5–10 clips per session.

---

### Workflow 4: Auto-Scheduler (Buffer / Publer)
```
Trigger: Google Sheets Row Updated (Video Final)
  → Buffer API or Publer API Node:
    → Upload video + caption + hashtags
    → Schedule per platform optimal times:
      - TikTok: Tue/Thu/Sat 7–9pm
      - YouTube Shorts: Daily 12pm
      - Instagram Reels: Mon/Wed/Fri 6–8pm
      - Facebook Reels: Mon/Thu 5–7pm
      - X: Tue/Thu 9–11am
  → Google Sheets Node: Update status to "Scheduled ✅"
```

---

## Tool Stack & Monthly Cost

| Tool | Purpose | Cost/mo |
|---|---|---|
| n8n (cloud) | Automation orchestration | $20 |
| ChatGPT Plus / API | Script generation | $20–40 |
| ElevenLabs | AI voiceover | $22 (Creator) |
| Runway ML | AI video generation | $95 (Standard — 625 credits) |
| CapCut Pro | Video editing | $10 |
| Buffer or Publer | Social scheduling | $18–25 |
| Epidemic Sound | Licensed music | $15 |
| Google Workspace | Storage + Sheets | $6 |
| Beehiiv (newsletter) | Email list for PM | $0–42 |
| Carrd | PM Landing page | $9/yr ≈ $1/mo |
| **TOTAL** | | **~$247–$276/mo** |

> Note: Original estimate was ~$360/mo. This is the lean version. Add Kajabi ($119/mo) when launching the course.

---

## Content Calendar Structure (Google Sheets)

| Column | Values |
|---|---|
| Date | Auto-filled |
| Niche | Masculinity / Satisfying |
| Theme | e.g., "Discipline", "Marble Flow" |
| Script | Full script text |
| Visual Prompt | Runway ML prompt |
| Voiceover Status | Pending / Generated / Approved |
| Video Status | Pending / Generated / Edited / Final |
| Caption | Final caption text |
| Hashtags | Full hashtag set |
| Platforms | TT / YT / IG / FB / X |
| Scheduled Time | Date + time per platform |
| Post Status | Scheduled / Posted / Analyzed |
| Notes | A/B test notes, performance flags |

---

## Weekly Operating Rhythm (Post-Automation)

| Day | Task | Time |
|---|---|---|
| Monday | Review AI-generated scripts for the week | 20 min |
| Tuesday | Approve voiceovers + review Runway clips | 20 min |
| Wednesday | Final edits in CapCut + approve scheduling queue | 30 min |
| Friday | Review analytics — note top performers | 20 min |
| Sunday | Plan next week's themes + update content calendar | 20 min |
| **TOTAL** | | **~90 min/wk** |

---

## Automation Build Order (Priority)

1. **Week 1:** Set up Google Sheets content calendar template
2. **Week 2:** Build n8n Script Generator workflow (ChatGPT → Sheets)
3. **Week 3:** Build ElevenLabs voiceover workflow
4. **Week 4:** Build Runway ML video generation workflow
5. **Week 5:** Build Buffer/Publer auto-scheduler workflow
6. **Week 6:** Connect all workflows + full end-to-end test
7. **Week 7–8:** Optimize + reduce manual touchpoints
