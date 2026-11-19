# ಗಾದೆ ಮಾತು | Gaade Maatu

**A Kannada proverb finder for everyday situations**

ಗಾದೆ ಮಾತು helps people find a Kannada proverb that fits a real-life situation. Describe what happened by typing or speaking in Kannada or English. The app returns one best-matching proverb, shows its meaning in both languages, explains why it fits in Kannada, and lets you hear the proverb aloud.

[Open the live app](https://gaadi-maatu-kannada.gableddisco16.chatgpt.site/) · [Download the source code](https://gaadi-maatu-kannada.gableddisco16.chatgpt.site/downloads/source.tar.gz)

## Features

- **Kannada and English input** through text or the microphone
- **One best-matching Kannada proverb** per search
- **Kannada and English meanings** with a Kannada explanation of how the proverb relates to the situation
- **Kannada audio playback** for the matched proverb
- **Searchable collection** of 233 proverbs, with filtering by proverb text or meaning
- **Kannada interface** with example situations to help first-time users get started

## How to use the app

1. Type a situation, select an example, or tap **🎙 ಸನ್ನಿವೇಶ ಹೇಳಿ** to speak.
2. For voice input, choose Kannada or English, allow microphone access, and check the transcribed text.
3. Press **ಗಾದೆ ಹುಡುಕಿ** to search.
4. Read the result or press **🔊 ಗಾದೆ ಕೇಳಿ** to hear the proverb.

Typing, recording, and selecting an example wait for the Search button before looking up a proverb. For microphone access, open the live HTTPS link in its own browser tab. Voice recognition depends on browser support, microphone permission, and the speech service or model. Text input is available throughout.

## Example

**Situation:** Meena earns little but buys a pricey phone on EMI.

**Matched proverb:** ಹಾಸಿಗೆ ಇದ್ದಷ್ಟು ಕಾಲು ಚಾಚು

**ಕನ್ನಡ ಅರ್ಥ:** ಆದಾಯಕ್ಕೆ ತಕ್ಕಂತೆ ಖರ್ಚು ಮಾಡಬೇಕು.

**English meaning:** Spend within your means.

**Why it fits:** Meena’s purchase puts pressure on a limited income. The proverb advises adjusting expenses to what you can afford.

## How matching works

The backend ranks proverbs using Kannada and English phrases, word overlap, and similarity to labeled Kannada situations. It returns the highest-ranked proverb when the match meets the relevance threshold. If the app finds no suitable match, it asks for more detail.

The interface uses HTML, CSS, and JavaScript, and the backend runs as a Cloudflare Worker. Voice input uses browser speech recognition where available. Recorded audio and uploaded audio files can be transcribed in a browser worker using Transformers.js and Whisper models.

## Project structure

| File or folder | Purpose |
| --- | --- |
| `page.mjs` | Webpage interface, styles, search controls, and audio player |
| `worker.mjs` | Website, search API, catalog API, and audio routes |
| `search.mjs` | Ranks proverbs against the input situation |
| `english.mjs` | English phrases used for matching |
| `corpus.mjs`, `additional-corpus.mjs` | Kannada proverbs, meanings, and examples |
| `english-meanings.mjs` | English meanings for the catalog |
| `explanation.mjs` | Kannada explanations for matched proverbs |
| `*-situations.mjs`, `situation-examples.mjs` | Labeled examples used by the matcher |
| `browser-asr.mjs` | Browser worker for audio transcription |
| `proverb-audio.mjs` | Kannada proverb audio clips used by the demo |
| `build.mjs` | Builds the deployable Worker |
| `submission/` | Dataset exporter, validation script, submission notes, and blank consent template |

## Build and verify

From the project folder, run these commands with Node.js installed:

```sh
npm run build
node submission/check.mjs
```

The build produces `dist/server/index.js` and its supporting modules. The validation script checks the challenge’s starter situations, selected Kannada and English inputs, bilingual meanings, the catalog, and audio responses.

## Evaluator dataset

The current **draft** contains 233 proverb entries, 504 labeled situations with at least two per entry, and 233 synthetic demo readings. To export the CSVs and **16 kHz mono WAV** files, install FFmpeg and run:

```sh
node submission/export.mjs ./team_XX/problem_02
```

Replace `XX` with your assigned team number. The output includes `gaade.csv`, `situations.csv`, `metadata.csv`, an `audio/` folder, a submission README, and a blank consent template.

### Dataset provenance and review status

The current draft draws on two supplied review CSVs, selected situation text from the supplied PDF, and a starter proverb from the challenge brief. Additional draft situations fill coverage gaps. The submission metadata flags synthetic recordings and tracks situation provenance.

The final evaluator submission still needs entries verified with elders or neighbors, regional or dialect information, human voice recordings, signed contributor consent, and peer review. Keep signed forms private and reference them by contributor code in the submission metadata. See the [submission notes](submission/README.md) for details.
