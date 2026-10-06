import pypandoc, os, textwrap

md = r"""# 🤖 AI ARMY — Free AI Stack for a Web Development & Digital Marketing Agency

**Updated:** September 29, 2026  
**Goal:** Build a large, mostly-free AI toolkit for web development, content marketing, SEO, social media, images, video, voiceovers, research, sales and automation.

> **Important:** “Free” does not always mean “unlimited” or “commercially licensed.” Free plans can have credits, watermarks, lower resolution, queues, usage caps, or different commercial-use terms. Check the provider's current terms before using an output in paid client work.

---

## 🧭 How to use this list

The rankings are **category rankings**, not a claim that one AI is objectively the best at everything.

- ⭐ = priority tool to test first
- 🆓 = has a $0/free access path
- 🔁 = recurring free allowance is available/has been reported
- 🧪 = free trial/limited starter credits rather than a strong recurring free tier
- 🖥️ = open/self-hosted option; hardware or setup is the trade-off
- ⚠️ = verify current commercial-use terms before client work

Free limits change frequently. Treat exact credit counts as a snapshot, not a permanent guarantee.

---

# 1. 💻 CODING / WEB DEVELOPMENT — TOP 10

| Rank | Tool / Model | Free access | Best use |
|---|---|---|---|
| 1 | ⭐ GitHub Copilot Free | 🆓 | IDE autocomplete, coding chat |
| 2 | ⭐ Cursor | 🆓 | AI-native coding/editor workflows |
| 3 | ⭐ Gemini coding tools / CLI ecosystem | 🆓 | Large-context coding and terminal workflows |
| 4 | ⭐ Cline | 🆓 🖥️ | Autonomous coding agent in VS Code |
| 5 | ⭐ Aider | 🆓 🖥️ | Terminal-based repo editing + Git |
| 6 | OpenCode | 🆓 🖥️ | Open coding-agent workflows |
| 7 | Continue | 🆓 🖥️ | Local/BYOK coding assistants |
| 8 | Zed + AI | 🆓 | Fast AI-enabled code editor |
| 9 | Windsurf / Devin Desktop ecosystem | 🆓 | Agentic development workflows |
| 10 | Amazon Q Developer | 🆓 | Coding help, AWS/developer workflows |

### Coding mission
Use multiple agents rather than depending on one:

**Planner → Coder → Reviewer → Tester → Security reviewer**

Example:
1. Use a general LLM to design the architecture.
2. Use Cursor/Copilot/Cline to implement.
3. Use Aider or another agent to refactor.
4. Ask a second model to review.
5. Run tests/lint/security checks yourself.

Recent 2026 roundups consistently identify tools such as Copilot, Cursor, Cline, Aider, Continue and other open coding agents as major free/BYOK options. Exact limits change, so verify the provider before standardizing your workflow.

---

# 2. 🧠 GENERAL AI / REASONING — TOP 10

| Rank | AI | Best agency use |
|---|---|---|
| 1 | ⭐ ChatGPT | Strategy, writing, research, coding, analysis |
| 2 | ⭐ Google Gemini | Research, multimodal work, Google ecosystem |
| 3 | ⭐ Claude | Long-form writing, reasoning, coding |
| 4 | ⭐ DeepSeek | Reasoning and coding |
| 5 | ⭐ Perplexity | Web research + citations |
| 6 | Grok | Current web/social-oriented research |
| 7 | Meta AI | Social/content ideation |
| 8 | Qwen | Multilingual/reasoning/coding |
| 9 | Mistral / Le Chat | General productivity |
| 10 | Microsoft Copilot | Microsoft ecosystem + productivity |

**Agency rule:** Don't ask one model to do everything. Cross-check important claims with a second model or primary source.

---

# 3. 🎨 AI IMAGE GENERATION — TOP 10

| Rank | Tool                               | Best use                                    |
| ---- | ---------------------------------- | ------------------------------------------- |
| 1    | ⭐ Gemini image generation          | General marketing imagery                   |
| 2    | ⭐ Ideogram                         | Posters, ads, typography/text in images     |
| 3    | ⭐ Leonardo AI                      | Marketing graphics + creative generation    |
| 4    | ⭐ Adobe Firefly                    | Brand/creative workflows                    |
| 5    | ⭐ FLUX                             | High-quality generation + technical control |
| 6    | Stable Diffusion                   | Local/self-hosted customization             |
| 7    | Krea                               | Fast creative iteration                     |
| 8    | Canva AI                           | Social posts + quick branded graphics       |
| 9    | Microsoft Designer / Image Creator | Quick marketing visuals                     |
| 10   | Playground-style image platforms   | Rapid concept generation                    |

### Image mission
For a marketing agency:

**Ideogram → text-heavy ads**  
**Leonardo/Krea → visual concepts**  
**Firefly → Adobe workflow**  
**FLUX/Stable Diffusion → advanced/local control**  
**Canva → final social graphic**

2026 free-image roundups commonly include Gemini, Ideogram, Leonardo, Firefly, Stable Diffusion/FLUX and Canva among the major free-access options. Free quotas and commercial rights vary by service.

---

# 4. 🎬 AI VIDEO GENERATION — TOP 20

This category is deliberately larger because video tools have very different strengths.

| Rank | Tool / Model                   | Best use                                                     |
| ---- | ------------------------------ | ------------------------------------------------------------ |
| 1    | ⭐ Kling                        | Cinematic motion / realistic short clips                     |
| 2    | ⭐ Hailuo AI                    | Realistic motion and short-form concepts                     |
| 3    | ⭐ Google Veo / Flow ecosystem  | High-end cinematic generation where free access is available |
| 4    | ⭐ Pika                         | Social effects and short creative clips                      |
| 5    | ⭐ Luma Dream Machine           | Image-to-video and rapid concepts                            |
| 6    | Runway                         | Professional creative/video workflows                        |
| 7    | PixVerse                       | Social/effect-heavy video                                    |
| 8    | Wan                            | Open/self-hosted video generation                            |
| 9    | HunyuanVideo ecosystem         | Open/self-hosted video                                       |
| 10   | LTX-Video                      | Open/local video workflows                                   |
| 11   | Genmo / Mochi ecosystem        | Open video experimentation                                   |
| 12   | Krea Video                     | Rapid visual experimentation                                 |
| 13   | CapCut AI                      | Social video + editing                                       |
| 14   | Canva AI video                 | Marketing/social content                                     |
| 15   | Lumen5                         | Blog/article → marketing video                               |
| 16   | Clipchamp AI tools             | Simple business video workflows                              |
| 17   | InVideo AI                     | Script → marketing video                                     |
| 18   | VEED AI                        | Social videos + editing                                      |
| 19   | Adobe Firefly video tools      | Adobe creative workflows                                     |
| 20   | Other open-source video models | Local experimentation                                        |

### Video mission

**Concept → Image → Animate → Edit → Voice → Captions → Publish**

A practical zero/low-cost stack:

`ChatGPT/Gemini → Ideogram/FLUX → Kling/Hailuo/Pika → CapCut → ElevenLabs/Fish Audio → captions`

### ⚠️ Video free-tier warning

Hosted video generation is one of the least predictable “free” categories. Free plans commonly use credits, queues, short clips, watermarks, or non-commercial restrictions. Open/self-hosted models can remove platform credit limits, but require suitable hardware or cloud compute.

Recent September 2026 comparisons specifically report free-access paths for Kling, Hailuo, Pika, Luma, Runway, PixVerse and open models such as Wan; exact allowances and commercial rights vary and change frequently.

---

# 5. 🎙️ AI VOICEOVER / TEXT-TO-SPEECH — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ ElevenLabs | Natural commercial-style voiceovers |
| 2 | ⭐ Fish Audio | Voice generation / multilingual work |
| 3 | Google AI Studio / Gemini voice ecosystem | Prototyping and multimodal audio |
| 4 | Microsoft Azure AI Speech | Business/TTS infrastructure |
| 5 | Amazon Polly | Developer/API workflows |
| 6 | OpenAI audio/voice tools | Conversational/audio workflows |
| 7 | PlayHT / PlayAI ecosystem | Voiceovers |
| 8 | Cartesia | Low-latency expressive speech |
| 9 | Hugging Face open TTS models | Local experimentation |
| 10 | Piper / open-source TTS | Local/offline generation |

### Voice mission

For short ads:

`Script → ElevenLabs/Fish Audio → CapCut → captions → export`

For scalable products:

`Your app → TTS API → audio storage → automated video pipeline`

⚠️ Voice cloning requires permission/rights from the person whose voice is being cloned. Don't clone a client's employee, celebrity, creator, or customer without appropriate authorization.

---

# 6. ✍️ COPYWRITING / CONTENT — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ ChatGPT | Full marketing copy workflow |
| 2 | ⭐ Claude | Long-form brand/content writing |
| 3 | ⭐ Gemini | Content + research |
| 4 | Jasper | Marketing workflows |
| 5 | Copy.ai | Sales/marketing copy workflows |
| 6 | Writesonic | SEO/content workflows |
| 7 | Rytr | Short-form copy |
| 8 | Grammarly AI | Editing and rewriting |
| 9 | QuillBot | Rewriting/paraphrasing |
| 10 | Notion AI | Workspace/content operations |

### Content production system

Create:

- Landing pages
- Service pages
- Blog posts
- LinkedIn posts
- Instagram captions
- Facebook posts
- X posts
- Email campaigns
- Ad variants
- Case studies
- FAQs
- Video scripts
- Lead magnets

**Do not publish raw AI text automatically.** Add brand voice, facts, examples, original insight and human QA.

---

# 7. 🔎 SEO / KEYWORD RESEARCH — TOP 10

| Rank | Tool | Main use |
|---|---|---|
| 1 | ⭐ Google Search Console | Real search performance |
| 2 | ⭐ Google Trends | Demand/trend discovery |
| 3 | ⭐ Ahrefs free tools | SEO research |
| 4 | ⭐ Semrush free tools | Keywords/competitors |
| 5 | Ubersuggest | Keyword research |
| 6 | AlsoAsked | Question/intent research |
| 7 | AnswerThePublic | Content ideas |
| 8 | Keyword Surfer | SERP keyword research |
| 9 | Google Keyword Planner | Ads + keyword demand |
| 10 | Perplexity | Research-assisted topic discovery |

### SEO mission

`Search Console → keyword research → SERP analysis → content brief → AI draft → human edit → internal links → publish → measure`

---

# 8. 🧪 AI RESEARCH / WEB RESEARCH — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ Perplexity | Search + cited answers |
| 2 | ⭐ ChatGPT | Research + synthesis |
| 3 | ⭐ Gemini | Web/multimodal research |
| 4 | Claude | Document analysis |
| 5 | NotebookLM | Source-grounded research |
| 6 | Google Search | Primary-source discovery |
| 7 | Microsoft Copilot | Web/productivity research |
| 8 | Grok | Current social/web-oriented discovery |
| 9 | Elicit | Research literature |
| 10 | Consensus | Evidence/research discovery |

**Rule:** For statistics, legal claims, pricing, product specifications and current events, open the primary source.

---

# 9. 📱 SOCIAL MEDIA CONTENT — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ Canva | Graphics + social designs |
| 2 | ⭐ CapCut | Reels/Shorts/TikTok editing |
| 3 | ⭐ ChatGPT | Hooks, captions, scripts |
| 4 | Gemini | Content ideation |
| 5 | Adobe Express | Branded social content |
| 6 | Buffer | Scheduling/workflows |
| 7 | Metricool | Scheduling + analytics |
| 8 | Later | Social planning |
| 9 | Meta Business Suite | Facebook/Instagram management |
| 10 | Publer | Multi-platform scheduling |

---

# 10. 🎯 AD CREATIVE / MARKETING DESIGN — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ Canva | Complete ad creative workflow |
| 2 | ⭐ Ideogram | Text-heavy advertising concepts |
| 3 | ⭐ Adobe Firefly | Creative generation |
| 4 | ⭐ Leonardo | Product/creative imagery |
| 5 | ChatGPT | Ad concepts + copy variants |
| 6 | Gemini | Creative brainstorming |
| 7 | Krea | Fast visual iteration |
| 8 | CapCut | Video ad variants |
| 9 | Meta Ads tools | Ad testing/management |
| 10 | Google Ads AI tools | Campaign/creative assistance |

---

# 11. 📊 ANALYTICS / DATA — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ Google Analytics | Website analytics |
| 2 | ⭐ Google Search Console | Organic search analytics |
| 3 | Looker Studio | Dashboards |
| 4 | Microsoft Clarity | Session/behavior analysis |
| 5 | ChatGPT | Data analysis |
| 6 | Gemini | Spreadsheet/data analysis |
| 7 | Claude | Large document/data analysis |
| 8 | Excel + Copilot | Business analysis |
| 9 | Google Sheets + AI tools | Lightweight analytics |
| 10 | Metabase | Self-hosted analytics |

---

# 12. 🤝 SALES / LEAD GENERATION — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ HubSpot free CRM | CRM + pipeline |
| 2 | ⭐ Apollo free tier | Prospecting |
| 3 | LinkedIn | B2B prospect discovery |
| 4 | Google Maps/Search | Local-business prospecting |
| 5 | Hunter | Email discovery |
| 6 | Instantly | Outreach workflows |
| 7 | Brevo | Email marketing |
| 8 | Mailchimp | Email campaigns |
| 9 | Tally | Lead forms |
| 10 | Calendly | Booking |

⚠️ Follow applicable anti-spam, privacy and platform rules. Personalize outreach instead of blasting identical AI-generated messages.

---

# 13. ⚙️ AUTOMATION — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ n8n | Powerful automation / self-hosting |
| 2 | ⭐ Make | Visual automation |
| 3 | Zapier | Easy integrations |
| 4 | GitHub Actions | Development automation |
| 5 | Google Apps Script | Google Workspace automation |
| 6 | Pipedream | Developer automation |
| 7 | IFTTT | Simple automation |
| 8 | Airtable automations | Database workflows |
| 9 | Notion automations | Content/project workflows |
| 10 | Webhooks + APIs | Custom automation |

---

# 14. 🧑‍💻 UI / WEBSITE DESIGN — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ Figma | UI/UX design |
| 2 | ⭐ v0 | UI/code generation |
| 3 | ⭐ Lovable | AI app/site prototyping |
| 4 | ⭐ Bolt | AI web development |
| 5 | Framer AI | Website design |
| 6 | Webflow AI | Website building |
| 7 | Relume | Sitemap/wireframe generation |
| 8 | Galileo-style AI design tools | UI concepts |
| 9 | Canva | Quick landing/social visuals |
| 10 | ChatGPT/Codex-style coding workflows | Custom websites |

---

# 15. 🧾 PRESENTATIONS / PROPOSALS — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ Gamma | AI presentations/docs |
| 2 | ⭐ Canva | Client decks |
| 3 | ChatGPT | Proposals/copy |
| 4 | Gemini | Presentation/content assistance |
| 5 | Claude | Long proposals |
| 6 | Microsoft PowerPoint + Copilot | Office workflows |
| 7 | Google Slides + Gemini | Workspace |
| 8 | Tome-style AI presentation tools | Storytelling |
| 9 | Beautiful.ai | Presentation design |
| 10 | Notion | Client docs/proposals |

---

# 16. 🖼️ LOGOS / BRANDING — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ Canva | Brand kits + social |
| 2 | ⭐ Adobe Express | Brand assets |
| 3 | Ideogram | Logo concepts |
| 4 | Leonardo | Visual exploration |
| 5 | Krea | Concept iteration |
| 6 | Figma | Final vector/UI work |
| 7 | Looka | Brand exploration |
| 8 | Adobe Firefly | Concept generation |
| 9 | ChatGPT | Brand strategy/naming |
| 10 | Gemini | Brand concept ideation |

**Important:** AI-generated logos can have originality/trademark issues. Perform a trademark search and create/edit final brand assets deliberately.

---

# 17. 🌍 TRANSLATION / LOCALIZATION — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ DeepL | High-quality translation |
| 2 | ⭐ Google Translate | Broad language coverage |
| 3 | ChatGPT | Contextual localization |
| 4 | Gemini | Multilingual content |
| 5 | Claude | Long-form localization |
| 6 | Microsoft Translator | Business translation |
| 7 | ModernMT | Translation workflows |
| 8 | Crowdin | Localization management |
| 9 | Lokalise | Product localization |
| 10 | Phrase | Enterprise localization |

For client websites, have a native/qualified reviewer check important marketing claims and culturally sensitive copy.

---

# 18. 🗣️ MEETINGS / TRANSCRIPTION — TOP 10

| Rank | Tool | Best use |
|---|---|---|
| 1 | ⭐ Otter.ai | Meeting transcription |
| 2 | ⭐ Fathom | Meeting notes |
| 3 | Fireflies.ai | Meeting capture |
| 4 | Notta | Transcription |
| 5 | Descript | Transcript + video editing |
| 6 | Whisper | Open/local transcription |
| 7 | Google Meet AI features | Workspace meetings |
| 8 | Zoom AI Companion | Meeting summaries |
| 9 | Microsoft Teams AI | Enterprise meetings |
| 10 | AssemblyAI | Developer/API transcription |

⚠️ Get appropriate consent before recording/transcribing meetings.

---

# 19. 🧠 PROMPT / KNOWLEDGE MANAGEMENT — TOP 10

| Rank | Tool                                            | Best use                       |
| ---- | ----------------------------------------------- | ------------------------------ |
| 1    | ⭐ ![[AI_Army_2026_Free_Tier_Web_Dev_Marketing]] | AI knowledge base              |
| 2    | ⭐ NotebookLM                                    | Source-grounded knowledge      |
| 3    | Google Drive                                    | Client documents               |
| 4    | Obsidian                                        | Local knowledge base           |
| 5    | GitHub                                          | Technical knowledge/versioning |
| 6    | Airtable                                        | Structured marketing data      |
| 7    | Tana                                            | Structured notes               |
| 8    | Anytype                                         | Local/private knowledge        |
| 9    | OneNote                                         | Research notes                 |
| 10   | Google Docs                                     | Collaborative client content   |

---

# 20. 🏗️ THE FREE AI AGENCY STACK

If you don't want 100 accounts, start here:

### 🧠 Brain
- ChatGPT
- Gemini
- Claude
- Perplexity

### 💻 Development
- GitHub Copilot Free
- Cursor
- Cline
- Aider

### 🎨 Images
- Ideogram
- Leonardo
- Firefly
- FLUX / Stable Diffusion

### 🎬 Video
- Kling
- Hailuo
- Pika
- Luma
- CapCut

### 🎙️ Voice
- ElevenLabs
- Fish Audio
- Open-source TTS

### ✍️ Content
- ChatGPT
- Claude
- Gemini
- Grammarly

### 🔎 SEO
- Search Console
- Google Trends
- Ahrefs free tools
- Semrush free tools

### 📊 Analytics
- GA4
- Search Console
- Clarity
- Looker Studio

### ⚙️ Automation
- n8n
- Make
- Zapier
- Apps Script

### 📱 Social
- Canva
- CapCut
- Meta Business Suite
- Buffer/Metricool

---

# 21. 🚀 CLIENT WEBSITE FACTORY

## Step 1 — Research

**Perplexity / Google / Gemini**

Collect:
- company information
- competitors
- customer pain points
- search intent
- services
- FAQs
- differentiators

## Step 2 — Strategy

**ChatGPT / Claude**

Generate:
- ICP
- positioning
- offer
- sitemap
- messaging
- CTA strategy
- SEO architecture

## Step 3 — Design

**Figma / Relume / v0 / Lovable**

Create:
- sitemap
- wireframes
- design system
- landing page
- mobile layouts

## Step 4 — Build

**Cursor / Copilot / Cline / Aider**

Build:
- frontend
- backend
- database
- forms
- auth
- integrations
- SEO
- analytics

## Step 5 — Images

**Ideogram / Leonardo / FLUX / Firefly**

Generate:
- hero imagery
- product concepts
- illustrations
- social graphics
- ad creatives

## Step 6 — Content

**ChatGPT / Claude / Gemini**

Create:
- landing copy
- service pages
- FAQs
- blog articles
- metadata
- social posts
- email sequences

## Step 7 — Video

**Kling / Hailuo / Pika / Luma + CapCut**

Create:
- website hero videos
- Reels
- Shorts
- TikTok
- ads
- product demos

## Step 8 — Voice

**ElevenLabs / Fish Audio**

Create:
- video narration
- ads
- explainers
- product demos

## Step 9 — SEO

**Search Console + Trends + SEO tools**

Do:
- indexing
- keyword mapping
- internal links
- schema
- technical SEO
- content updates

## Step 10 — Measure

**GA4 + Search Console + Clarity + Looker Studio**

Track:
- traffic
- leads
- conversions
- organic clicks
- rankings
- landing-page behavior

---

# 22. 📣 ONE CLIENT → 30+ PIECES OF CONTENT

From one website/project:

1. Homepage copy
2. About page
3. 5 service pages
4. 5 SEO articles
5. 10 LinkedIn posts
6. 10 Instagram captions
7. 10 X posts
8. 5 short videos
9. 5 video scripts
10. 5 ad concepts
11. 5 ad images
12. 3 email campaigns
13. 1 lead magnet
14. 1 case study
15. FAQ database

**One core idea → many formats.**

---

# 23. 🔥 SHORT-FORM CONTENT FACTORY

Use:

**ChatGPT**
→ hook

**Claude/Gemini**
→ script refinement

**Ideogram/Leonardo**
→ visuals

**Kling/Hailuo/Pika**
→ motion

**ElevenLabs/Fish Audio**
→ narration

**CapCut**
→ edit + captions

**Canva**
→ thumbnail

**Buffer/Meta Business Suite**
→ schedule

---

# 24. 💰 HOW TO KEEP IT $0 AS LONG AS POSSIBLE

### Use free hosted tiers for:
- research
- writing
- coding
- simple images
- small video tests
- voice experiments

### Use open-source/local tools when:
- you need large volume
- you need privacy
- hosted credits become the bottleneck
- you have capable hardware

### Don't optimize only for “unlimited”
The cheapest tool can become expensive in **time**.

Track:

`Cost = subscription + API/compute + editing time + QA time`

---

# 25. ⚠️ COMMERCIAL CLIENT CHECKLIST

Before delivering AI-generated material:

- [ ] Check the current free-plan license.
- [ ] Check commercial-use restrictions.
- [ ] Check whether attribution is required.
- [ ] Check whether watermarks are present.
- [ ] Check whether generated voices require additional rights.
- [ ] Don't clone a person's voice without authorization.
- [ ] Don't generate copyrighted characters/logos for deceptive use.
- [ ] Don't copy competitors' protected branding.
- [ ] Verify factual claims.
- [ ] Human-review important client content.
- [ ] Keep project/source files when possible.
- [ ] Document which AI tools were used.

---

# 26. 🧪 AI ARMY OPERATING PRINCIPLE

Don't build an agency around one model.

Build a **pipeline of specialized workers**:

```text
                 ┌──────────────┐
                 │   STRATEGY   │
                 │ ChatGPT etc. │
                 └──────┬───────┘
                        ↓
              ┌──────────────────┐
              │     RESEARCH     │
              │ Perplexity/GS    │
              └────────┬─────────┘
                       ↓
              ┌──────────────────┐
              │     CONTENT      │
              │ Claude/Gemini    │
              └────────┬─────────┘
                       ↓
       ┌───────────────┼────────────────┐
       ↓               ↓                ↓
   ┌────────┐     ┌─────────┐      ┌────────┐
   │ CODING │     │ IMAGES  │      │ VIDEO  │
   │ Cline  │     │ Ideogram│      │ Kling  │
   └────┬───┘     └────┬────┘      └───┬────┘
        │              │                │
        └──────────────┼────────────────┘
                       ↓
                 ┌────────────┐
                 │   VOICE    │
                 │ ElevenLabs │
                 └─────┬──────┘
                       ↓
                 ┌────────────┐
                 │   EDITING  │
                 │   CapCut   │
                 └─────┬──────┘
                       ↓
                 ┌────────────┐
                 │ DISTRIBUTE │
                 │ Social/SEO │
                 └─────┬──────┘
                       ↓
                 ┌────────────┐
                 │ ANALYTICS  │
                 │ GA4/Clarity│
                 └────────────┘