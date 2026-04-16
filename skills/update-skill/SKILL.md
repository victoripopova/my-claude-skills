---
name: update-skill
description: >
  Use this skill when the user wants to update, replace, or install a Claude skill
  from a downloaded .skill file into their local Claude Code setup and GitHub repo.
  Triggers include: "update my skill", "install updated skill", "replace skill",
  "I downloaded a new version of a skill", "push skill to GitHub", or any mention
  of a .skill file and wanting it to be available in Claude Code.
---

# Update Skill in Claude Code + GitHub

This skill installs or replaces a skill from a downloaded `.skill` file into
`~/my-claude-skills/skills/` and pushes the update to GitHub.

---

## Step 1 — Find the .skill file

Check what `.skill` files are available in Downloads:

```bash
ls ~/Downloads/*.skill
```

If there are multiple, ask the user which one they want to install.
If there's only one, proceed with it.

---

## Step 2 — Get the skill name

Extract the skill name from the filename (e.g. `user-interview-transcription.skill`
→ skill name is `user-interview-transcription`).

Confirm with the user before proceeding if there's any ambiguity.

---

## Step 3 — Remove old version and unpack new one

```bash
rm -rf ~/my-claude-skills/skills/<skill-name>
cd ~/my-claude-skills/skills
unzip ~/Downloads/<skill-name>.skill
```

Then verify it unpacked correctly:
```bash
ls ~/my-claude-skills/skills/<skill-name>
```

You should see `SKILL.md` listed. If not, stop and tell the user something went wrong.

---

## Step 4 — Push to GitHub

Compare the old and new versions to write the commit message yourself:

```bash
git -C ~/my-claude-skills diff skills/<skill-name>/SKILL.md
```

Read the diff and summarise what changed in one short sentence. Examples:
- "remove follow-up section, embed quotes inside bullets"
- "fix file naming format to DD-MM-YY"
- "add speaker detection for demo-style interviews"

Then commit with your summary:
```bash
cd ~/my-claude-skills
git pull
git add .
git commit -m "update <skill-name>: <your summary>"
git push
```

---

## Step 5 — Confirm

Tell the user:
- Which skill was updated
- That Claude Code can now use the new version immediately
- That the change is saved to GitHub

---

## Edge Cases

| Situation | How to handle |
|---|---|
| No `.skill` file found in Downloads | Ask the user to download it from Claude.ai first |
| Skill doesn't exist yet (new install) | Skip the `rm -rf` step, just unzip and push |
| Git push fails | Run `git pull` first then retry push; if still failing, show the error to the user |
| Multiple `.skill` files in Downloads | List them and ask the user which one to install |
