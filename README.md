# claude-welcome

Onboarding pro **Slevomat AI tooling** — Claude Code plugin který provede nového kolegu kompletním setupem dev prostředí.

## Komu je to určeno

- **Dev / BI inženýr** — chystáš se na dbt / Snowflake / Streamlit projekty ve Slevomat. ✅ Jsi v cílovce.
- **Analytik / data konzument** — máš jen číst hotové marty, nechceš programovat? Tohle pro tebe není. (Napiš Andrému — konzumentský onboarding je TODO.)
- **Product / PM / marketing** — neprogramuješ? Použij standardní Claude Cowork bez specifických Slevomat pluginů.

## Jak na to

### 1. Nainstaluj Claude Code

Ze **[claude.ai/download](https://claude.ai/download)** stáhni Claude Desktop nebo Claude Code pro svou platformu. Spusť a přihlas se **firemním Slevomat accountem**.

### 2. Přidej marketplace a nainstaluj plugin

V Claude spusť:

```
/plugin marketplace add AndreHeller/claude-welcome
/plugin install onboarding@claude-welcome
```

### 3. Spusť onboarding

```
/welcome
```

Claude tě provede kompletním setupem — WSL, SSH klíč, git, registrace Slevomat marketplace, první projekt. Počítej s 30–60 minutami (většinou čekání na instalace).

## Co je v plánu (obsahu pluginu)

- `welcome` — uvítání, detekce stavu (OS, WSL, git, SSH), rozcestník ✅
- `install-wsl` — WSL2 + Ubuntu pro Windows, hloubkový tutor ✅
- `setup-ssh` — co je SSH klíč, vygenerování, upload do GitLabu (TODO)
- `setup-git` — git config (pull.rebase, user.email), naše konvence (TODO)
- `install-slevomat-marketplace` — registrace privátního Slevomat GitLab marketplace do settings.json (TODO)
- `first-project` — clone dbt repo, chain na projektový `/onboarding-dbt` skill (TODO)
- `troubleshoot` — typické gotchy (TODO)

Aktuálně v alpha fázi — první 2 skills k testování.

## Pro Claude.ai admin: deploy do Slevomat Cowork org

Pokud máš **Owner/Primary Owner** roli v Slevomat Claude org, můžeš plugin deployovat do org marketplace:

1. Claude Desktop → **Organization Settings** → **Plugins** → **Add plugin**.
2. Vyber **GitHub sync** → zadej `AndreHeller/claude-welcome`.
3. Visibility: `Installed by default` pro všechny dev kolegy (nebo `Available for install`).
4. Kolegové v Slevomat org uvidí plugin v Claude Desktop *Browse plugins*.

## Development

Pro lokální test:

```bash
git clone git@github.com:AndreHeller/claude-welcome.git
cd claude-welcome
# V Claude Code:
# /plugin marketplace add ./claude-welcome
# /plugin install onboarding@claude-welcome
# /welcome
```

## Kontakt

- Owner: André Heller — `andre.heller@slevomat.cz`
- GitHub: [AndreHeller/claude-welcome](https://github.com/AndreHeller/claude-welcome)

## Licence

Internal use (Slevomat). Viz LICENSE pokud se to později změní.
