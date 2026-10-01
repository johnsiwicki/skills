# Treehouse Skills

This repository is a [Claude Code plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces) named `treehouse`. It packages one plugin, `treehouse-skills`: CMS-safe frontend work, conversion-rate testing, website QA, marketing-tag audits, and YouTube thumbnail design.

## Install in Claude Code

Inside a Claude Code session:

```
/plugin marketplace add johnsiwicki/skills
/plugin install treehouse-skills@treehouse
```

`treehouse` is the marketplace name in `.claude-plugin/marketplace.json`. `treehouse-skills` is the plugin name. The install id is `plugin@marketplace`.

After install, skills are namespaced under the plugin, for example `/treehouse-skills:tracking-pixel-audit`.

The same marketplace can be registered from a shell with `claude plugin marketplace add johnsiwicki/skills`, then `claude plugin install treehouse-skills@treehouse`.

## Compatibility

Claude Code plugins do not work natively with Cursor, Grok Bot, or most other agent systems. The `.claude-plugin` marketplace and plugin manifests, and the `/plugin` install flow above, are Claude-specific. Other agents will not read `marketplace.json` or `plugin.json`, and they will not apply the `treehouse-skills:` namespace.

What does transfer is the skill content. Each skill is a directory at `plugins/treehouse-skills/skills/<name>/SKILL.md`. That markdown can often be copied, or lightly adapted, into Cursor skills or another agent skill format. Packaging differs: copy the skill directory, including supporting files such as `site-builder/references/` and `site-builder/assets/`, and place it where that system loads skills.

## Skills

| Skill | Purpose |
| --- | --- |
| `site-builder` | Build responsive, accessible homepage and landing-page sections for ATB and Treehouse CMS templates (`borders.php`, `template.css`, `homepage.js`). |
| `ab-testing-cro` | Generate lead-gen A/B test ideas from a URL, scored with the ICE framework. |
| `tracking-pixel-audit` | Inspect a URL and report which marketing/tracking tags are present (GTM, GA4, Google Ads, and common pixels). |
| `website-qa-audit` | Repeatable QA pass: Lighthouse scores, Core Web Vitals, mobile friendliness, and severity-ranked visual defects across mobile and desktop viewports. |
| `youtube-thumbnail-creator` | Design high-CTR YouTube thumbnails incorporating a logo. |

## Layout

```
.claude-plugin/marketplace.json                 # marketplace catalog (name: treehouse)
plugins/treehouse-skills/
  .claude-plugin/plugin.json                    # plugin manifest (name, version, description)
  skills/<name>/SKILL.md                        # one directory per skill
  skills/site-builder/references/               # ATB / Treehouse CMS edit contract
  skills/site-builder/assets/atb-template/      # bundled baseline: borders.php, template.css, homepage.js
  skills/site-builder/agents/openai.yaml        # Codex-style interface metadata for site-builder
```

Claude Code loads skills from the default `skills/` directory at the plugin root, so `plugin.json` leaves `skills` unset. That directory sits beside `.claude-plugin/`, not inside it.

## Validate and version

Validate the marketplace and the plugin manifest with `claude plugin validate .` before pushing.

The plugin version is `0.3.0` in `plugins/treehouse-skills/.claude-plugin/plugin.json`. Because that field is set, installed copies update only when it changes. Bump `version` on every release that should reach people who already installed the plugin. It is set only in `plugin.json` (not also on the marketplace entry), which is what Claude Code uses.
