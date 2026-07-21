# Voxtral Dictation

A Raycast extension for speech-to-text dictation powered by [Mistral's Voxtral](https://mistral.ai/news/voxtral/) API. Speak into your microphone and have the transcription pasted wherever your cursor is.

## Features

- **Dictate** — Toggle recording with a single shortcut. Press once to start, press again to stop and paste the transcription at your cursor.
- **Reformulate** — Open a comparison view showing the raw transcription alongside a cleaned-up version (via Mistral Chat). Choose which to paste.
- **Customizable reformulation prompt** — Configure the system prompt used for reformulation in the extension preferences.

## Prerequisites

- [Raycast](https://raycast.com)
- [SoX](http://sox.sourceforge.net/) for microphone recording:
  ```
  brew install sox
  ```
- A [Mistral AI API key](https://console.mistral.ai/)
- Microphone permission for Raycast (System Settings > Privacy & Security > Microphone)

## Setup

1. Clone this repo and install dependencies:
   ```
   git clone https://github.com/chloedia/voxtral-dictation.git
   cd voxtral-dictation
   npm install
   ```

2. Start in development mode:
   ```
   npm run dev
   ```

3. In Raycast, search for **Dictate** — it will prompt for your Mistral API key on first use.

4. Assign keyboard shortcuts in Raycast:
   - **Dictate** — e.g. `Cmd+Shift+Space` (toggle recording on/off)
   - **Reformulate Last Dictation** — e.g. `Cmd+Shift+R` (review & choose version)

## Commands

| Command | Mode | Description |
|---------|------|-------------|
| **Dictate** | no-view | Toggle: start recording, or stop and paste transcription |
| **Reformulate Last Dictation** | view | Compare raw vs reformulated text, then paste your choice |

## How it works

1. **Recording** — Uses SoX (`rec`) to capture 16-bit mono WAV audio at 16kHz via a detached background process.
2. **Transcription** — Sends the audio to `POST https://api.mistral.ai/v1/audio/transcriptions` using the `voxtral-mini-latest` model.
3. **Pasting** — Uses Raycast's `Clipboard.paste()` to insert text at the current cursor position.
4. **Reformulation** — Sends the raw transcription to `POST https://api.mistral.ai/v1/chat/completions` using `mistral-small-latest` with a configurable system prompt.

## Project structure

```
src/
  shared.ts        # Shared constants, types, and helpers
  dictate.tsx       # Dictate command (record + transcribe + paste)
  reformulate.tsx   # Reformulate command (compare + choose + paste)
assets/
  icon.png          # Extension icon
package.json        # Raycast manifest, preferences, and dependencies
```

## License

MIT

```
================================================================================
                          CEASE AND DESIST NOTICE
                 COPYRIGHT INFRINGEMENT & DEMAND FOR TAKEDOWN
================================================================================

TO:      The Management of [Insert Infringing Website Name/URL Here]
FROM:    Danial Zivehdar
DATE:    July 19, 2026
SUBJECT: URGENT: Unauthorized Use of Intellectual Property and Demand for 
         Immediate Removal

Dear Sir/Madam,

This is a formal legal notice to inform you that your website has engaged in 
the unauthorized copying, replication, and use of the design, patterns, links, 
and content belonging to me, Danial Zivehdar. 

COMPREHENSIVE RIGHTS RESERVATION:
Please be formally notified that under the website's governing terms and 
applicable intellectual property laws, I retain exclusive and absolute ownership 
of ALL rights, titles, and interests regarding this project. This includes, 
but is not limited to, the website contract/terms, all designs, templates, 
hyperlinks, source codes, and absolutely ALL associated content and digital 
assets (hereinafter referred to as "the Protected Assets"). Any unauthorized 
use, reproduction, or distribution of these Protected Assets constitutes a 
material breach of copyright, contractual terms, and digital property laws.

Therefore, you are hereby formally demanded to take the following actions 
within 12 hours [or specify 12 days] from the receipt of this notice:

1. IMMEDIATE CESSATION: Immediately cease and desist from any further use, 
   display, or distribution of the Protected Assets.
   
2. COMPLETE DATA SANITIZATION: Permanently delete and purge all copied files 
   and assets from your servers, virtual environments, mobile device storage, 
   and any other associated data storage systems without exception.
   
3. WEBSITE TAKEDOWN: Immediately shut down or disable access to the infringing 
   sections of your website until the violations are fully resolved and a 
   final legal determination is made.

Please be advised that failure to comply with this notice within the stipulated 
timeframe will leave me with no choice but to pursue all available legal 
remedies. This includes, but is not limited to, filing formal complaints with 
the relevant judicial authorities and cyber police, as well as submitting a 
formal DMCA/copyright infringement report to your Hosting Provider and Domain 
Registrar to request the immediate suspension and takedown of your entire 
website.

Furthermore, be advised that no informal guarantees, settlements, or 
communications will be entertained regarding this matter. Any necessary 
correspondence will be conducted strictly through official legal channels.

All of my legal rights and remedies are expressly reserved.

Sincerely,

----------------------------------------
Danial Zivehdar
Phone: +98 9197159411
Email: danialzivehdar1992@gmail.com
----------------------------------------
================================================================================
