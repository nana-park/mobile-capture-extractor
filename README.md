# Mobile Capture Extractor

**Sync phone screenshots and automatically organize them in Notion.**

Take a screenshot on your phone.

Let your configured sync and Codex automation handle the next steps.

This is a **Codex skill for an automated workflow**.

It is not a standalone phone app.

## How it works

1. Your Galaxy phone syncs screenshots to OneDrive.
2. A Codex automation checks the synced inbox.
3. Codex reads new screenshots and groups pages from the same post.
4. It saves notes and original images to Notion.
5. If you have allowed cleanup, it removes verified originals and checks that deletion syncs back to your phone.

**Set up phone sync, Notion access, and a Codex automation first.**

Installing this skill alone does not turn them on.

Once set up, screenshots are picked up from the synced inbox.

You do not need to send each image in a chat.

## What comes out?

- Text read from the screenshots.
- Source links, when they can be found.
- Short summaries.
- Original images attached to the notes.
- Questions about anything unclear.

For example:

> **Input:** 3 screenshots of one article.
>
> **Result:** 1 Notion note with the text, summary, and all 3 images.
>
> **Needs review:** The last sentence is cut off.
>
> **Cleanup:** Keep the originals until the saved images have been checked.

Charts and tables can also be saved as separate crops.

The original images are kept with the record.

## Try one batch first

```text
$mobile-capture-extractor
Check my synced screenshots inbox.
Use the pm-job profile.
Save up to 5 screenshots to my connected Notion database.
Keep the originals for this first test.
Tell me what worked and what needs review.
```

The included `pm-job` profile organizes AI, IT, robotics, and mobility material.

It adds topics, keywords, summaries, and questions to think about.

## Good to know

Blurry text can be read incorrectly.

Missing text is not filled in by guessing.

Source links may be unavailable.

Cleanup needs your permission and successful save checks.

Files that need review or failed to save stay in the inbox.

Keep screenshots, private notes, and processing logs out of this public repository.

<details>
<summary>Setup, automation, and safety details</summary>

### Install the skill

Put all files in `.agents/skills/mobile-capture-extractor` inside your project.

Compare any existing installation before replacing it.

If you use Git:

```sh
git clone https://github.com/nana-park/mobile-capture-extractor.git .agents/skills/mobile-capture-extractor
```

Open the project in Codex and check that the skill is available.

Keep `references/profiles/pm-job.md` in its existing location.

### Connect the workflow

Set up Galaxy-to-OneDrive screenshot sync.

Make the synced inbox available to Codex.

Connect your Notion destination and allow image uploads.

Configure a recurring Codex automation to run this skill.

Choose your own schedule and check its timezone.

Codex needs access to the files and connected services when the automation runs.

The repository does not include a sync client, OCR engine, credentials, or a background service.

### Existing setup example

The inspected workspace uses a OneDrive folder named `screenshots-inbox`.

An active Codex automation is configured for 09:00 and 18:00.

Its configuration does not explicitly specify a timezone.

It checks new screenshots first, then older unprocessed files.

Each run handles up to 10 images.

It saves results to a Notion database and keeps a private local processing ledger.

Failed items are marked for retry.

Deletion sync is checked on a later run.

This is an example of an external setup, not a schedule bundled with this skill.

The phone's live sync settings and end-to-end execution were not tested for this README update.

### Cleanup rules

The core skill requires explicit permission for deletion and deletion sync.

The profile's automatic cleanup wording is not permission from a new user.

For archived screenshots, verify the note, original attachment, reopening, and file match before deletion.

Test deletion sync on a small sample before a large batch.

Keep unclear files and failed uploads.

The included profile also describes removing reviewed, out-of-scope files.

Agree on that policy before enabling cleanup.

Some environments cannot use the profile's image clipboard upload method.

Do not mark an item complete if its saved original cannot be reopened.

### Files

- `SKILL.md`: extraction, grouping, verification, and cleanup rules.
- `references/profiles/pm-job.md`: classification and Notion layout.

The source had no `agents/` folder.

Only these files were copied from `nana-park/skills` at commit `875982c984d8fd7f40931826dc4a73ff67e1e5cb`.

Other skills, personal data, and the original Git history were not copied.

</details>
