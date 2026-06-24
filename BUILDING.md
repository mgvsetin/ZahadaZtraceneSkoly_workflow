# Jak udělat spustitelnou aplikaci (.exe)

## Úvod

Chceš svůj Python projekt změnit na aplikaci, kterou můžeš spustit bez instalace Pythonu? Stačí kliknout na soubor `.exe` a aplikace se spustí. Tento návod ti to vysvětlí.

## Krok 1: Instalace PyInstalleru

PyInstaller je nástroj, který převede Python kód na spustitelný soubor.

```powershell
pip install pyinstaller
```

## Krok 2: Spuštění build skriptu

V projektu máš soubor `build.py`. Stačí ho spustit:

```powershell
python build.py
```

To je vše! Skript si zkontroluje, že je PyInstaller nainstalován, a pak vytvoří aplikaci.

## Krok 3: Kde najdu výsledek?

Po spuštění `build.py` se vytvoří:

```
dist/
└── ZahadaZtraceneSkoly/
    ├── ZahadaZtraceneSkoly.exe          ← Tady je tvá aplikace!
    ├── python311.dll                      (podporující soubory)
    ├── library.zip                        (balíčky)
    └── ...
```

Teď můžeš:
- **Spustit aplikaci:** Dvojklik na `ZahadaZtraceneSkoly.exe`
- **Poslat kamarádům:** Zkopíruj si celou složku `ZahadaZtraceneSkoly/` a pošli mu ji
- **Spustit odkudkoliv:** `ZahadaZtraceneSkoly.exe` funguje bez instalace Pythonu

## Krok 4: Přizpůsobení (volitelné)

Chceš-li změnit jméno, ikonu nebo chování aplikace, otevři `build.py` a uprav konstanty na začátku:

```python
PROJECT_NAME = "MujeAplikace"           # Jméno aplikace
ENTRY_POINT = "main.py"                 # Hlavní Python soubor
PROJECT_ICON = "moje_ikona.ico"         # Volitelně ikona
CONSOLE_MODE = True                     # True = vidět terminál, False = skryt
```

Pak znovu spusť `python build.py`.

## FAQ

**Q: Jak velký je výsledný soubor?**  
A: Typicky 50–150 MB (záleží na počtu knihoven a kódu).

**Q: Funguje to na Macu/Linuxu?**  
A: `pyinstaller --onedir main.py` vytvoří aplikaci pro daný OS. Chceš-li `.exe` na Windowsu, musíš spouštět na Windowsu.

**Q: Mohu ji poslat jako `.zip`?**  
A: Ano! Zkomprimuj si složku `dist/ZahadaZtraceneSkoly/` do `.zip`, pošli, on si ji rozbali a spustí.

**Q: Jak se zbavím složek `build/` a `.spec` souborů?**  
A: Nejsou potřeba. Smažeš je, při příštím buildování se znova vytvoří. Důležitá je jenom složka `dist/`.

**Q: Jak přidám ikonu?**  
A: Měj soubor `icon.ico` a v `build.py` nastav `PROJECT_ICON = "icon.ico"`.

## Tipy

- **Testuj na čistém počítači:** Zjistíš, jestli aplikace opravdu funguje bez Pythonu
- **Přidej do `.gitignore`:** `dist/`, `build/`, `*.spec` – není třeba je commitovat
- **Verze:** Když vydáš novou verzi, znova spusť `python build.py`
