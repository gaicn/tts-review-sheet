# Multilingual Translation & Pronunciation Review Sheet

An offline, single-file review sheet for **native-speaker human reviewers** who need to verify that
deliverable translations and their spoken pronunciation are correct — line by line, with a visible
audit trail.

Originally built for proofreading TTS announcement scripts (place names, nouns and short phrases),
the sheet now supports **19 delivery languages** and an optional AI-assisted cross-check.

## The problem it solves

A translation can be textually correct while a text-to-speech engine still reads a name wrong:
polyphonic characters, place names, numbers inside phone announcements, or romanisation leftovers.
Browser speech synthesis only accepts the string you hand it — there is no API to "pin" the
pronunciation of one character. This sheet keeps the deliverable text untouched and instead uses a
separate **pronunciation read-as string** that is sent to the local TTS voice. The reviewer hears
the corrected reading immediately, then records the decision in the notes column as work evidence.

## Who it is for

Native-speaker human reviewers only. The tool does **not** generate translations, does **not**
decide which answer is correct, and does **not** replace human judgement. An optional AI assist may
suggest candidate translations and candidate readings with confidence and authority hints; the
reviewer always chooses the final answer.

## What it does

- Line-by-line log: source text, deliverable translation, a pronunciation "read-as" string,
  local TTS preview (male / female voice, rate), problem type, revision, notes, and a
  "manually reviewed" checkbox that locks the row against accidental edits.
- 19 selectable delivery languages. The choice updates the column label, the local TTS language
  and the customer-facing report together; existing table data is left unchanged.
- Import from a pasted tab-separated block; export CSV, a full JSON backup, and a read-only
  **customer delivery report** (English HTML, no editor controls, no network references).
- 8 interface languages.
- Optional **AI-assisted review**: bring your own endpoint / model / API key, stored only on this
  machine. The AI returns candidate answers; the human adopts one or dismisses them.
- An opt-in **version check** with one-click download of a newer file, plus a small feedback card
  in the footer.

## Privacy and network behaviour

| Action | Network |
|---|---|
| Reviewing, TTS preview, import / export, delivery report | None — works fully offline |
| Clicking the footer version, then "Check for a newer version" | Read-only GETs to public version sources |
| Clicking "Download newer version" | Read-only GET of the new HTML file; the downloaded bytes are checked to actually embed the announced version before being saved |
| Enabling AI assist | Only the current row's source / translation / read-as text is sent to **your own** configured endpoint |
| Clicking the GitHub link or email in the feedback card | Opens an external page / mail client — only when you click |

Table data, notes and review flags are stored in this browser's `localStorage` only and are never
uploaded by the tool. The customer delivery report is a static, read-only export with no scripts
that contact the network.

> If you select a voice your browser labels "network", your browser may send the preview string to
> its own speech service. Use a local voice for sensitive material.

## Getting started

1. Download `tts-review.html` from the [latest release](https://github.com/gaicn/tts-review-sheet/releases/latest).
2. Open it in a modern Chromium-based browser — double-click is enough. No server, no install,
   no build step, no dependencies.
3. Choose the delivery language and the interface language.
4. Paste a tab-separated source / translation block into the import area, or edit rows directly.
5. Preview each line, adjust the read-as string, then tick "manually reviewed" to lock the row.
6. Export a JSON backup regularly, and export the customer delivery view when finished.

Before replacing the file with a newer version, export a JSON backup and import it into the new
file. Settings and data are designed to carry over.

## Updating

The footer shows the current version. Click it, then "Check for a newer version (requires
internet)". If a newer release exists, a download button saves the new HTML into your browser's
download folder. Replace the old file with it and import your JSON backup. Every release also has a
changelog under [Releases](https://github.com/gaicn/tts-review-sheet/releases).

## Feedback

- GitHub issues: <https://github.com/gaicn/tts-review-sheet/issues>
- Email: <feedbug@foxmail.com>

Please do not paste client translations, place names under NDA, or any other sensitive material
into a public issue.

## Files in this repository

- `tts-review.html` — the complete tool, one self-contained file with all CSS and JS inline.
- `version.json` — the version number read by the tool's opt-in update check.

No build step, no dependencies, no telemetry.
