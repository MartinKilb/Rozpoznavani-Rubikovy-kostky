# Rozpoznávání Rubikovy kostky
tým: Martin Kilbergr, Michaela Skálová, vedení: Ing. Miroslav Jiřík, Ph. D. \
předmět: KKY/PUIA4 \
datum: 27. 5. 2025 \

---
---

# Úvod
Rubikova kostka je bezesporu nejznámější hlavolam na světě. Rozpoznávání jejích stran (jednotlivých barevných samolepek) je užitečná úloha především pro tyto účely:
- Jejich počítačová reprezentace se používá jako vstup pro roboty, které ji skládají.
- Na soutěžích ve skládání Rubikovy kostky na čas [(WCA)](https://www.worldcubeassociation.org/) se kontroluje správnost rozložení kostky podle obrázku scramblu (zatím však pouze manuálně).

Tento projekt vznikl jednak z osobního zájmu o počítačové vidění a Rubikovu kostku, dále jako příležitost vyzkoušet si dvě různé cesty k řešení reálného problému. Cílem je vytvořit jednoduchý systém, který rozpozná, zda je strana Rubikovy kostky složená, nebo ne. Po rozpoznání všech 6 stran vyhodnotí, zda je složena i celá kostka.

Budou otestovány dvě odlišné metody:
1. **Klasické metody počítačového vidění** – manuální zpracování obrazu a klasifikace pomocí běžných nástrojů počítačového vidění (opencv).
2. [**Teachable Machine**](https://teachablemachine.withgoogle.com/) – nástroj od společnosti Google, který umožňuje trénovat modely i bez programování.

Obě metody následně porovnáme z hlediska složitosti, robustnosti a přesnosti.

---

# Model #2 – použití klasických metod počítačového vidění
Rozhodli jsme se vytvořit dva modely pomocí klasických metod, každý trochu odlišný, pro různé účely. \
První z nich operuje pouze s mřížkou, do které uživatel kostku umístí a před použitím zkalibruje. \
[Klikněte pro otevření modelu #2a v Google Colab](https://colab.research.google.com/github/MartinKilb/Rozpoznavani-Rubikovy-kostky/blob/bcbf52fa9b717f7abb8193236e0fcfebb8946cab/model_klasicky_pristup_s_mrizkou.ipynb) \
Druhý z nich se pokouší o rozmazání pozadí a použití Houghovy transformace. \
[Klikněte pro otevření modelu #2b v Google Colab](https://colab.research.google.com/github/MartinKilb/Rozpoznavani-Rubikovy-kostky/blob/bcbf52fa9b717f7abb8193236e0fcfebb8946cab/model_klasicky_pristup_s_Houghovo_transformaci.ipynb)

---

# Porovnání přístupů

Klasický (ne-ML) přístup se ukázal jako spolehlivější díky možnosti kontrolovat jednotlivé kroky – zejména barevnou kalibraci. Ani konvoluční neuronová síť (Teachable machine) si nevedla špatně – s přesností kolem 90 % na dvou různých testovacích sadách. Pokud bychom projekt dělali znovu, smysluplné by bylo využít neuronku jen pro lokalizaci kostky v obraze, ale zbytek pipeline řešit klasicky – např. určení barev a reprezentaci stavu.

---

# Problémy řešení

Zásadní roli hrálo osvětlení a ukázalo se jako problém napříč všemi variantami řešení. Problémy nastaly také s automatickým odstraňováním pozadí – nástoj rembg a následná segmentace kůže nefungovaly dostatečně spolehlivě, proto jsme nakonec použili rozmazávání od středu.
3D rekonstrukci ze tří stran nebo jiné pohledy z úhlů jsme kvůli složitosti a časovým důvodům vůbec neimplementovali.

---

## Možná rozšíření

- Automatická lokalizace kostky kdekoliv v obraze.
- Rozpoznávání barev a stavu kostky z krátkého videa.
- Robustní podpora různých typů Rubikových kostek (např. jiné tvary).
- Pořízení většího množství trénovacích dat.

---

## Závěr

Na začátku úkol působil jako jednoduchý a přímočarý. V praxi se ale ukázal jako technicky náročný, plný neočekávaných problémů. Vývoj ukázal, že spolehlivá
a správná detekce Rubikovy kostky není vůbec elementární úloha, což jsme si původně mysleli. Dále jsme si uvědomili, jak důležité je definovat si jasný cíl hned na počátku projektu.
