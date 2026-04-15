---
name: install-wsl
description: "Hloubkový tutoriál pro instalaci WSL2 + Ubuntu na Windows. Použij pro nové kolegy na Windows kteří ještě WSL nemají, nebo pro opravu rozbité instalace. Vysvětlí co WSL je, proč ho potřebujeme pro Slevomat dev práci, provede krok-za-krokem instalaci včetně první konfigurace Unix user accountu."
---

# WSL 2 + Ubuntu — instalace a první setup

Tohle je pravděpodobně **nejdelší krok** celého onboardingu (~15 minut včetně restartu). Projdeme si to pečlivě — když WSL funguje správně, všechno další je snadné.

## Co je WSL a proč ho používáme

**WSL** (Windows Subsystem for Linux) je **Linux uvnitř Windows** — běží plný Linux kernel (jádro) bez rebootu, bez virtualizace přes VMware/VirtualBox, bez dual boot. Prakticky:

- Máš Windows. Otevřeš *Ubuntu* z Start menu. Dostaneš Linux terminál.
- Ve Windows editoruješ soubory (např. VS Code). V terminálu WSL spouštíš příkazy (`python`, `dbt`, `git`). **Sdílí to samé disk**.
- Nepotřebuješ dual boot ani VM — je to **nativní Windows feature** od Microsoftu.

**Proč to pro Slevomat potřebujeme:**

1. **dbt + Snowflake + Python ekosystém** běží v Linux/macOS-first světě. Na čistých Windows narazíš na subtilní bugy (path separators, file permissions, shebangy). WSL odstraňuje 95 % těchto problémů.
2. **Bash, SSH, git** v Linux kontextu jsou "zlatý standard" pro dev tutoriály a dokumentaci. Budeš vidět příkazy jako `source .venv/bin/activate` — ty fungují v WSL out-of-box.
3. **Claude Code extension pro VS Code** ve WSL remote módu je nejčistší dev setup. Claude "žije" ve WSL (má shell access na Linux), VS Code "žije" na Windows (rychlé UI).

**Co WSL není**: nejsou to Docker kontejnery. Je to jako lehká VM s tight Windows integrací. Pro nás rozdíl není podstatný — používáme ho jako Linux.

## Prerequisites — zkontroluj před instalací

### 1. Verze Windows

WSL2 potřebuje **Windows 10 build 19041+ (2004 release)** nebo **Windows 11**. Jak zkontrolovat:

```powershell
winver
```

Okno ukáže build. Pokud starší, nejdřív **Windows update**, pak pokračuj.

### 2. Virtualizace v BIOSu

WSL2 pod kapotou používá Hyper-V virtualizaci. Musí být povolená v BIOSu (obvykle je, ale pozor u starších strojů).

**Check** (PowerShell admin):

```powershell
systeminfo | Select-String "Hyper-V"
```

Mělo by ukázat:
```
Hyper-V Requirements: VM Monitor Mode Extensions:    Yes
                      Virtualization Enabled In Firmware: Yes
```

Pokud `No`, restartuj, jdi do BIOSu (obvykle F2/F10/Del při startu), najdi *Virtualization* / *VT-x* / *AMD-V* → Enable → Save. Pokud se nevyznáš, napiš Andrému nebo IT.

### 3. Administrátorská práva

Instalace WSL vyžaduje admin. Musíš spouštět **PowerShell jako Administrator** (pravým klik → *Run as administrator*).

## Instalace — hlavní command

**V PowerShellu jako Administrator:**

```powershell
wsl --install -d Ubuntu-22.04
```

Co se stane:

1. **Stáhne se** Windows Subsystem for Linux feature.
2. **Stáhne se** Ubuntu 22.04 distribuce (~500 MB).
3. **Instaluje se** WSL kernel.
4. **Může vyžadovat restart** (Windows ti to řekne).

Po restartu se **automaticky otevře** okno Ubuntu terminálu s výzvou:

```
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username:
```

### První setup Unix usera

**Jméno**: doporučuji lowercase, bez diakritiky, bez mezer. Např. `vaclav`, `michal`, `andre`. **Toto je jméno jen v Linux světě** — nemusí matchovat tvůj Windows username.

**Heslo**: 
- Musíš ho zapamatovat (bude potřeba pro `sudo` příkazy — povýšení na roota).
- Nepiš tam totéž co máš na Windows/firemní heslo. Generuj nové.
- Když píšeš heslo, **neuvidíš hvězdičky ani znaky** (Linux konvence) — prostě piš a dej Enter.

Po potvrzení se objeví prompt `<jmeno>@<hostname>:~$` — jsi v Ubuntu! 🎉

## Verifikace že WSL běží správně

**V Ubuntu terminálu**:

```bash
# Kernel version — musí být 5.x+ (WSL2)
uname -r

# Distro
lsb_release -a

# Python (Ubuntu 22.04 má Python 3.10 default, budeme potřebovat 3.12+)
python3 --version
```

**Zpět v PowerShell (ne admin stačí)**:

```powershell
# Ubuntu musí být "Running" a ve "VERSION 2"
wsl --list --verbose
```

Očekávaný výstup:
```
  NAME            STATE           VERSION
* Ubuntu-22.04    Running         2
```

## Instalace Python 3.12 (pokud Ubuntu má jen 3.10)

Ubuntu 22.04 default obsahuje Python 3.10. Pro Slevomat dbt potřebujeme 3.12+. V Ubuntu terminálu:

```bash
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.12 python3.12-venv
python3.12 --version   # ověření
```

`sudo` se zeptá na tvé Unix heslo (to co jsi zadal při prvním setupu).

## Gotcha: shebang bind u venv

**Varování pro budoucnost:** když později budeš vytvářet Python venv (`python3 -m venv .venv`), binárky uvnitř (`pip`, `dbt`) si zapamatují **absolutní cestu** k Python interpreteru. Pokud přejmenuješ / přesuneš složku projektu, venv se **rozbije** (`cannot execute: required file not found`). Řešení: `rm -rf .venv && python3 -m venv .venv && pip install ...` = rebuild. Tohle si nemusíš pamatovat teď, jen vědět že to existuje.

## Co dál

Pokud všechny verifikace prošly, **máš Linux**. Super. Další krok je **SSH klíč** — potřebujeme ho pro přístup k Slevomat GitLab repům.

**Teď napiš: `/setup-ssh`** (v Claude nebo spusť skill ručně).

Pokud verifikace **selhaly** (WSL list ukáže VERSION 1, Ubuntu nenaběhla, atd.), napiš mi výstupy a poradím — WSL issues jsou obvykle BIOS virtualizace, starý Windows, nebo corporate policy co blokuje Hyper-V.

## Troubleshooting nejčastější chyby

| Chyba | Příčina | Řešení |
|---|---|---|
| `WslRegisterDistribution failed with error: 0x8007019e` | WSL feature nenainstalováno | `wsl --install` znovu v admin PS |
| `Error code: Wsl/Service/0x80040326` | Hyper-V disabled | Zapnout v BIOSu (viz výše) |
| `WslRegisterDistribution failed with error: 0x800701bc` | Starý kernel | `wsl --update` v admin PS |
| Ubuntu terminál se hned zavře | Corrupt install | `wsl --unregister Ubuntu-22.04` + znovu install |
| `VERSION` je `1`, ne `2` | Default je WSL1 | `wsl --set-default-version 2` + reinstall distro |

Kdybys narazil na něco jiného, napiš mi chybový text + výstup `wsl --status`. Pojďme to vyřešit spolu.
