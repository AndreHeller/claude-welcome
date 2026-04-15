---
name: welcome
description: "Vítací skill Slevomat AI onboardingu. Použij jako první krok pro každého nového kolegu — provede ho detekcí stavu (Windows/macOS/Linux, Claude Code klient, již nastavené věci) a nabídne rozcestník na další skills. Auto-invoke když uživatel řekne 'jsem nový', 'onboarding', 'setup Slevomat', 'jak začít'."
---

# Vítej ve Slevomat AI onboardingu 👋

Tenhle plugin tě provede kompletním setupem dev prostředí pro práci na Slevomat BI projektech. Je to tutoriál — vysvětlíme **co** děláme i **proč**, ne jen seznam příkazů. Počítej s 30–60 minutami práce (většinou čekání na instalace).

## Co budeme společně dělat

```
1. Zjistíme co máš                    ← teď
2. WSL + Ubuntu (jen Windows users)   → /install-wsl
3. SSH klíč + upload na GitLab/GitHub → /setup-ssh
4. Git konfigurace                    → /setup-git
5. Registrace Slevomat marketplace    → /install-slevomat-marketplace
6. První projekt (dbt repo)           → /first-project
```

## Nejdřív status check — pojďme zjistit kde jsi

Prosím spusť tyto příkazy a ukaž mi výstup:

### Windows (PowerShell nebo cmd)

```powershell
# Verze Windows (musí být Windows 10 2004+ nebo Windows 11)
winver

# Status WSL
wsl --status
wsl --list --verbose
```

### macOS nebo Linux nativně

```bash
# Verze OS
uname -a

# Python 3.12+ dostupný?
python3 --version
```

### Univerzální (kde jsi aktuálně)

```bash
# Kde spouštíš Claude Code?
# - "Claude Desktop" (native aplikace z claude.ai)
# - "VS Code + Claude extension"
# - "Terminal CLI (claude)"
echo "I am running in: <doplň podle situace>"
```

## Po výstupu rozhodnu další krok

Podle výstupu tě nasměruju:

- **Windows bez WSL** → spustíme `/install-wsl` (~15 min, zahrnuje restart).
- **Windows s WSL, ale bez Ubuntu** → `/install-wsl` dodělá distro.
- **Windows s WSL + Ubuntu už běžícím** → přeskočíme na `/setup-ssh`.
- **macOS / nativní Linux** → přeskočíme WSL celé, přímo `/setup-ssh`.

## Kdo jsi

Pokud jsi:

- **Dev (BI inženýr, dbt, Snowflake, Streamlit)** → pokračuj celým flow. Jsi v cílovce.
- **Analytik / data konzument bez dbt** → tento plugin je hlavně pro dev. Pro konzumentský flow (jen čtení martů, Streamlit dashboardy) ještě plugin neexistuje. Napiš Andrému, dostane prioritu.
- **Product / PM** → zatím nemáme onboarding plugin. Pro obecný Claude Cowork stačí standardní onboarding Slevomat AI admin.

## Důvěřuj postupu

Tohle je hloubkový tutorial — u každého kroku vysvětlíme **co to je** a **proč** (SSH klíč, git rebase, Snowflake profile, …). Když něco nechápeš, **zeptej se mě**. Nespěchej a nepřeskakuj kroky — budoucí ty si poděkuješ.

Až mi ukážeš výstup příkazů výše, naskočím do dalšího kroku.
