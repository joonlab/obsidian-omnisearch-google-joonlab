# Obsidian Omnisearch in Google — JoonLab

A Tampermonkey/Violentmonkey **userscript** that injects [Obsidian](https://obsidian.md)
[Omnisearch](https://github.com/scambier/obsidian-omnisearch) results into the Google
search sidebar — multi-vault, relevance bars, real body previews + tags via Local REST
API, per-vault colors, themes, keyboard navigation.

This is **박준 (JoonLab)'s personal fork**, maintained for my own setup and customizations.

## Credit / lineage

- **Original** — Simon Cambier's *"Inject Omnisearch results into your search engine"*
  ([scambier/userscripts](https://github.com/scambier/userscripts), part of the
  [Omnisearch](https://github.com/scambier/obsidian-omnisearch) project).
- **Base fork** — 구요한 (CMDSPACE):
  [johnfkoo951/obsidian-omnisearch-google-cmds](https://github.com/johnfkoo951/obsidian-omnisearch-google-cmds)
  — multi-vault fan-out, Local REST enrichment, themes, UI.
- **This fork** — 박준 (JoonLab): the changes below + rebrand.

All credit for the concept and the heavy lifting goes to the upstream authors. MIT
(see `LICENSE`), attribution retained.

## What this fork changes (vs. CMDS base)

1. **Open each result in a NEW Obsidian tab** — clicking a card no longer overwrites the
   previously opened note. Uses Local REST API's `POST /open/{path}?newLeaf=true`.
2. **Bring Obsidian to the foreground on open** — after the REST open succeeds, the
   `obsidian://open` deeplink is fired to raise the Obsidian window (it focuses the
   already-open tab, so no duplicate is created). On REST failure, the deeplink opens
   the note directly as before.
3. **Rebrand** — name / author / widget header → JoonLab.

## Install

1. Install [Tampermonkey](https://www.tampermonkey.net/) in your browser. On Chromium
   138+ (Chrome/Arc): extension Details → **Allow user scripts** ON, **Site access** =
   On all sites.
2. Install the script (raw):
   **[`obsidian-omnisearch-google-joonlab.user.js`](https://raw.githubusercontent.com/joonlab/obsidian-omnisearch-google-joonlab/main/obsidian-omnisearch-google-joonlab.user.js)**
3. In Obsidian, enable **Omnisearch** → its HTTP server (one port per vault). For body
   previews + accurate tags + reliable new-tab open, also enable
   [Local REST API](https://github.com/coddingtonbear/obsidian-local-rest-api)'s
   non-encrypted (HTTP) server per vault.
4. Configure via the widget's `⋯` button on any Google results page.

## My setup (reference)

| Vault | Omnisearch HTTP | Local REST (HTTP) |
|---|---|---|
| joonlab-default | 51361 | 27123 |
| CMDS_JoonLab | 51362 | 27125 |

General: **Use Local REST API for body + tags** = ON. Common parent folder of vaults set
so "copy abs path" works. Both vault windows must stay open for both to answer.

## Updating without losing settings

Tampermonkey settings (vault ports/keys/toggles) are bound to the installed script's
internal id, not its name. To pick up a new version **after editing this repo**, use
Tampermonkey → **"Check for userscript updates"** — it updates the existing script in
place (by `@updateURL`), so your settings are preserved. (Re-opening the raw URL after a
name change would create a *second* script instead; prefer "Check for updates".)
