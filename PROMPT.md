# Onboarding prompt pro Claude Desktop (Windows users)

Tento prompt copy-paste do **Claude Desktop chatu** (native aplikace z [claude.ai/download](https://claude.ai/download), přihlášený Slevomat firemním emailem).

Claude buď stáhne hloubkový WSL install tutoriál z tohoto repa automaticky, nebo si tě navede k ručnímu zkopírování. Tak jako tak tě provede setupem krok za krokem.

---

```
Ahoj, jsem nový Slevomat AI kolega. Na svém Windows potřebuju nainstalovat WSL2 + Ubuntu, VS Code s Remote-WSL extension, a Claude Code extension v WSL kontextu.

Stáhni prosím obsah tohoto souboru z GitHubu:

https://github.com/AndreHeller/claude-welcome/blob/main/plugins/wsl-onboarding/skills/install-wsl/SKILL.md

Pokud k té URL nemáš přístup (Claude Desktop často nemá web fetch), řekni mi to a já si URL otevřu sám v browseru a obsah ti zkopíruju sem do chatu jako moji další zprávu.

Pak postupuj přesně podle toho obsahu — tutoriál stylem, krok po kroku, vysvětluj co a proč, počkej na moji reakci a teprve pak pokračuj. Jsem noob, nespěchej a nic nepředpokládej.

Cíl: po dokončení mám funkční WSL + Ubuntu + Unix user + VS Code v WSL mode + Claude Code extension přihlášenou. Pak mě navedeš na další plugin (dev-onboarding) v Claude Code extension pro SSH, git, Slevomat marketplace.
```

---

## Co dělat když Claude říká že nemůže fetchovat

To je běžný scénář — Claude Desktop má často omezený nebo žádný web fetch (firemní firewall, výchozí restrikce). Postup:

1. Otevři v browseru: https://github.com/AndreHeller/claude-welcome/blob/main/plugins/wsl-onboarding/skills/install-wsl/SKILL.md
2. Klikni vpravo nahoře na **Raw** tlačítko (zobrazí čistý markdown bez GitHub UI).
3. Ctrl+A → Ctrl+C (zkopíruj celý obsah).
4. Vrať se do Claude Desktop chatu.
5. Vlož obsah jako další zprávu (Ctrl+V → Enter). Můžeš přidat větu typu: *"Tady je obsah toho SKILL.md — postupuj podle něj."*

Claude pak má kompletní tutoriál v kontextu a může tě vést.

## Co se stane potom

Po dokončení tohoto flow budeš v **VS Code** se **Claude Code extension** ve **WSL mode**. Skill `install-wsl` ti na konci řekne:

> *"Otevři Claude Code extension chat panel. Napiš:*  
> *'Nainstaluj mi prosím plugin `dev-onboarding@claude-welcome` z `https://github.com/AndreHeller/claude-welcome` a spusť skill `welcome` — ať mě provede SSH, git a Slevomat setupem.'"*

Plugin `dev-onboarding` (skills v této chvíli ještě dopisujeme) tě dovede skrz:
- SSH klíč generaci a upload do GitLab + GitHub.
- Git config (pull.rebase, user.email, atd.).
- Instalaci `gh` (GitHub CLI) a `glab` (GitLab CLI).
- Vysvětlení Claude konceptů: memory, CLAUDE.md, skills — co je kde, na co sahat, na co ne.
- Registraci privátního Slevomat marketplace + instalaci org-wide `bi` pluginu.
- "Klonuj projekt na kterém chceš pracovat — jeho lokální CLAUDE.md a skills tě povedou dál."

## Pro budoucnost: plugin install v Claude Desktop přes Cowork admin

Až bude tento flow stabilní a `dev-onboarding` plugin kompletní, plánujeme nasazení do **Slevomat Cowork private plugin marketplace** (Anthropic Enterprise feature). Kolegové v Slevomat Claude org pak uvidí pluginy přímo v Claude Desktop **Browse plugins** modálu — bez fetchování markdown URL, bez manual copy, bez ručního setupu.

Pro tu chvíli ale platí: **fetch URL přístup** s **manual copy fallback**, jednoduchý a fungující.
