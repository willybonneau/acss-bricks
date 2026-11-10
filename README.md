# acss-bricks

by / par **Willy Bonneau**

[English](#english) · [Français](#français)

---

## English

A Claude Code skill that makes **Automatic.css 4 (ACSS 4.x)** the default framework for every WordPress + Bricks Builder site: ACSS settings, variables, classes and recipes are always used, and ACSS 3.x syntax is never applied.

### What it does

- Reads the target site's real ACSS state before writing: Bricks design context through MCP, the generated `automatic.css` file, or WP-CLI (`wp acss ...`).
- Lets the agent change **any ACSS setting except breakpoints**, which stay read-only in both ACSS and Bricks.
- Uses ACSS 4 variables (`--primary`, `--space-m`, `--section-space-l`, `--grid-3`, `--grid-gap`, `--h2`, `--text-m`, …) instead of hard-coded values.
- Uses only the reduced ACSS 4 class set (`.section--l`, `.bg--dark`, `.btn--primary`, `.text--l`, `.smart-spacing`, …). Everything else goes into custom BEM classes.
- Uses ACSS 4 recipes (`?auto-grid`, `?center-all`, `?btn`, …) in Bricks custom CSS.
- Blocks removed ACSS 3.x names (`.grid--3`, `.padding--m`, `--action`, `-trans-*`, `@recipe`, …).

### Requirements

- [Claude Code](https://claude.com/claude-code)
- WordPress + Bricks Builder 2.4+ with Automatic.css 4.x
- Recommended: [Bricks Skills](https://github.com/codeerhq/bricks-skills) and the WordPress MCP Adapter (the skill refers to `bricks:*` skills and Bricks abilities)
- Optional: WP-CLI for `wp acss` commands

### Installation

```bash
git clone https://github.com/willybonneau/acss-bricks.git ~/.claude/skills/acss-bricks
```

On Windows, `~` is `C:\Users\<you>`. Then run `/reload-plugins` or start a new chat. The skill loads automatically for WordPress + Bricks work, or you can call it with `/acss-bricks`.

### Update

```bash
cd ~/.claude/skills/acss-bricks && git pull
```

Then run `/reload-plugins` or start a new chat.

### Refresh the skill after an ACSS documentation update

Paste this prompt into Claude Code, ideally with the site's MCP connected. Replace `<URL>` with a site running the latest ACSS version:

```
Update the acss-bricks skill (~/.claude/skills/acss-bricks/SKILL.md)
following the ACSS documentation update.

1. Run git pull in the skill folder.
2. Re-read the ACSS 4 docs: https://docs.automaticcss.com and https://docs.automaticcss.com/cli
   (colors, assignments, typography, spacing, smart spacing, grids,
   buttons, icons, recipes, CLI commands).
3. Compare with a real site's state: bricks-get-design-context (summary)
   and the generated CSS /wp-content/uploads/automatic-css/automatic.css of the site <URL>.
4. Show me the list of differences (additions, renames, removals)
   before changing anything.
5. After approval: edit SKILL.md, keep ACSS 4 only, keep the rule
   "every setting can be changed except breakpoints",
   and add any obsolete name to the forbidden list.
6. Update the README if needed (EN + FR), then commit and push.
```

Step 6 pushes to this repository. If you don't have write access, fork it first and clone your fork.

### Sources

- ACSS 4 documentation: https://docs.automaticcss.com
- ACSS CLI: https://docs.automaticcss.com/cli

The site itself is the source of truth. If an ACSS option is disabled in the dashboard, its class or variable is not generated, and the agent checks for this before writing.

### License

[MIT](LICENSE) © 2026 Willy Bonneau

### Disclaimer

This is a community skill, not affiliated with Automatic.css or Bricks Builder. Test on a staging site first.

---

## Français

Une compétence Claude Code qui fait d'**Automatic.css 4 (ACSS 4.x)** le framework par défaut de chaque site WordPress + Bricks Builder : les réglages, variables, classes et recipes ACSS sont toujours utilisés, et la syntaxe ACSS 3.x n'est jamais appliquée.

### Ce qu'elle fait

- Lit l'état ACSS réel du site cible avant d'écrire : contexte de design Bricks via MCP, fichier `automatic.css` généré, ou WP-CLI (`wp acss ...`).
- Permet à l'agent de modifier **tous les paramètres ACSS sauf les points de rupture**, qui restent en lecture seule dans ACSS comme dans Bricks.
- Utilise les variables ACSS 4 (`--primary`, `--space-m`, `--section-space-l`, `--grid-3`, `--grid-gap`, `--h2`, `--text-m`…) au lieu de valeurs en dur.
- N'utilise que le jeu réduit de classes ACSS 4 (`.section--l`, `.bg--dark`, `.btn--primary`, `.text--l`, `.smart-spacing`…). Tout le reste passe par des classes BEM custom.
- Utilise les recipes ACSS 4 (`?auto-grid`, `?center-all`, `?btn`…) dans le CSS custom de Bricks.
- Bloque les noms ACSS 3.x supprimés (`.grid--3`, `.padding--m`, `--action`, `-trans-*`, `@recipe`…).

### Prérequis

- [Claude Code](https://claude.com/claude-code)
- WordPress + Bricks Builder 2.4+ avec Automatic.css 4.x
- Recommandé : [Bricks Skills](https://github.com/codeerhq/bricks-skills) et le WordPress MCP Adapter (la compétence renvoie aux compétences `bricks:*` et aux abilities Bricks)
- Optionnel : WP-CLI pour les commandes `wp acss`

### Installation

```bash
git clone https://github.com/willybonneau/acss-bricks.git ~/.claude/skills/acss-bricks
```

Sous Windows, `~` correspond à `C:\Users\<vous>`. Lancez ensuite `/reload-plugins` ou ouvrez un nouveau chat. La compétence se charge automatiquement pour le travail WordPress + Bricks, ou s'appelle avec `/acss-bricks`.

### Mise à jour

```bash
cd ~/.claude/skills/acss-bricks && git pull
```

Puis `/reload-plugins` ou un nouveau chat.

### Actualiser la compétence après une mise à jour de la doc ACSS

Collez ce prompt dans Claude Code, idéalement avec le MCP du site connecté. Remplacez `<URL>` par un site qui a la dernière version d'ACSS :

```
Mets à jour la compétence acss-bricks (~/.claude/skills/acss-bricks/SKILL.md)
suite à la mise à jour de la documentation ACSS.

1. git pull dans le dossier de la compétence.
2. Relis la doc ACSS 4 : https://docs.automaticcss.com et https://docs.automaticcss.com/cli
   (couleurs, assignations, typographie, espacements, smart spacing, grilles,
   boutons, icônes, recipes, commandes CLI).
3. Compare avec l'état réel d'un site : bricks-get-design-context (summary)
   et le CSS généré /wp-content/uploads/automatic-css/automatic.css du site <URL>.
4. Montre-moi la liste des différences (ajouts, renommages, suppressions)
   avant de modifier quoi que ce soit.
5. Après validation : édite SKILL.md, garde ACSS 4 uniquement, garde la règle
   "tous les paramètres modifiables sauf les points de rupture",
   et ajoute aux interdits tout nom devenu obsolète.
6. Mets le README à jour si besoin (EN + FR), puis commit et push.
```

L'étape 6 pousse vers ce dépôt. Sans droit d'écriture, faites d'abord un fork et clonez votre fork.

### Sources

- Documentation ACSS 4 : https://docs.automaticcss.com
- CLI ACSS : https://docs.automaticcss.com/cli

Le site fait foi. Si une option ACSS est désactivée dans le dashboard, sa classe ou sa variable n'est pas générée, et l'agent le vérifie avant d'écrire.

### Licence

[MIT](LICENSE) © 2026 Willy Bonneau

### Avertissement

Compétence communautaire, non affiliée à Automatic.css ni à Bricks Builder. À tester d'abord sur un site de préproduction.
