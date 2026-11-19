# Šablóna záverečnej práce PEVŠ FI v LaTeXu
[![CC0](https://img.shields.io/badge/License-CC0-lightgrey.svg)](http://creativecommons.org/publicdomain/zero/1.0/)

Oficiálna LaTeX šablóna bakalárskej a diplomovej práce na [Paneurópskej vysokej škole](https://www.paneurouni.com), Fakulte informatiky.

## Vlastnosti

- 📚 Bibliografia podľa normy STN ISO 690
- 🔧 Jednoduché prispôsobenie
- 🤖 Automatické generovanie zoznamov
- 📝 Podpora zoznamu skratiek (glossaries)
- 🖼️ Správa obrázkov
- 💻 Podpora výpisov zdrojového kódu

## Požiadavky

- Distribúcia LaTeXu – odporúčame **TeX Live** v plnej inštalácii (na macOS sa volá **MacTeX**)
- VS Code (voliteľné)

## Inštalácia LaTeXu

Šablóna potrebuje `pdflatex`, `biber` a `makeglossaries`. Všetky sú súčasťou plnej inštalácie TeX Live, preto ju odporúčame na všetkých systémoch.

### Windows

1. Stiahnite inštalátor [install-tl-windows.exe](https://mirror.ctan.org/systems/texlive/tlnet/install-tl-windows.exe).
2. Spustite ho a nechajte zvolenú plnú schému (*full scheme*). Inštalácia trvá dlhšie a sťahuje niekoľko GB.
3. Inštalátor pridá TeX Live do systémovej cesty (PATH). Po inštalácii otvorte **nové** okno PowerShellu alebo príkazového riadka.

TeX Live pre Windows obsahuje vlastný Perl, takže `makeglossaries` funguje bez ďalšej inštalácie. Podrobnosti sú na stránke [TeX Live on Windows](https://tug.org/texlive/windows.html).

### macOS

Nainštalujte MacTeX jedným zo spôsobov:

- stiahnite [MacTeX.pkg](https://mirror.ctan.org/systems/mac/mactex/MacTeX.pkg) a spustite ho (viac na [tug.org/mactex](https://www.tug.org/mactex/)), alebo
- cez [Homebrew](https://brew.sh):
  ```bash
  brew install --cask mactex
  ```

Po inštalácii otvorte nové okno Terminálu. Ak `biber` hlási chybu, pozrite časť [Riešenie problémov](#riešenie-problémov).

### Linux

**Debian / Ubuntu:**
```bash
sudo apt update
sudo apt install texlive-full
```

**Fedora:**
```bash
sudo dnf install texlive-scheme-full
```

**Iné distribúcie:** použite oficiálny inštalátor podľa návodu [TeX Live – quick install](https://tug.org/texlive/quickinstall.html).

### Overenie inštalácie

Na všetkých systémoch spustite v termináli (Windows: PowerShell):
```bash
pdflatex --version
biber --version
makeglossaries --version
```
Každý príkaz má vypísať verziu. Ak systém príkaz nenájde, otvorte nové okno terminálu alebo skontrolujte PATH.

## Nastavenie

### Získanie šablóny
Šablónu môžete získať dvoma spôsobmi:

1. **Použitie ako šablóny** (odporúčané)
   - Otvorte [GitHub repozitár](https://github.com/PEVS-FI/thesis-template)
   - Vpravo hore kliknite na zelené tlačidlo „Use this template“
   - Zvoľte „Create a new repository“
   - Podľa pokynov vytvorte vlastný repozitár

2. **Stiahnutie vydania**
   - Otvorte [GitHub repozitár](https://github.com/PEVS-FI/thesis-template)
   - Stiahnite najnovšie vydanie (release)
   - Rozbaľte stiahnutý súbor na zvolené miesto

### Úprava obsahu
Po získaní šablóny:

- Upravte `metadata.tex` a vyplňte metadáta; dbajte na správny typ práce podľa štúdia (bakalárska/diplomová)
- Nahraďte `essentials/assignment.pdf` vlastným zadaním
- Do `essentials/abstract.tex` napíšte abstrakt
- Podľa potreby upravte `essentials/acknowledgment.tex` a `essentials/declaration.tex`

> **Poznámka**: Ak nemáte konzultanta, nechajte riadok *Consultant* v `metadata.tex` zakomentovaný.

> **Poznámka**: Text čestného vyhlásenia (vrátane vyhlásenia o použití nástrojov umelej inteligencie) je v `lang/slovak.tex` a `lang/english.tex` v makre `\lndeclarationtext`. Súbor `essentials/declaration.tex` ho iba vykresľuje.


### Nastavenie VS Code

1. Nainštalujte rozšírenie LaTeX Workshop
2. Nastavte citačný backend na `biblatex`
3. Pridajte `makeglossaries` a `biber` do `latex-workshop.latex.tools`
4. Pridajte recept zostavenia do `latex-workshop.latex.recipes`

Príklad receptu:
```json
{
    "name": "pdflatex ➞ makeglossaries ➞ biber ➞ pdflatex × 2",
    "tools": [
        "pdflatex",
        "makeglossaries",
        "biber",
        "pdflatex",
        "pdflatex"
    ]
} 
```
Ak chcete pre dokument použiť konkrétny recept, pridajte na začiatok `main.tex` tento riadok (*recipe-name* nahraďte názvom receptu):
```tex
%!LW recipe=recipe-name
```

### Zostavenie dokumentu

Použite tlačidlo Build v rozšírení LaTeX Workshop vo VS Code, alebo v priečinku projektu (tam, kde je `main.tex`) spustite:

```bash
pdflatex main
makeglossaries main
biber main
pdflatex main
pdflatex main
```

Príkazy sú rovnaké na Windows (PowerShell aj príkazový riadok), macOS aj Linuxe. Výsledkom je súbor `main.pdf`.

### Štruktúra projektu

```
.
├── essentials/            
│   ├── abstract.tex       # Abstrakt SK/EN
│   ├── acknowledgment.tex # Poďakovanie
│   ├── acronyms.tex       # Zoznam skratiek
│   ├── appendices.tex     # Zoznam príloh
│   ├── bibliography.bib   # Použitá literatúra
│   ├── declaration.tex    # Čestné vyhlásenie autora
│   ├── titlepage.tex      # Hlavná titulná strana
│   ├── titlepage-alt.tex  # Druhá titulná strana
│   └── assignment.pdf     # Zadanie
├── examples/              
│   └── examples.tex       # Ukážky použitia
├── lang/              
│   ├── english.tex        # Anglická jazyková mutácia
│   └── slovak.tex         # Slovenská jazyková mutácia
├── metadata.tex           # Metadáta práce
├── main.tex               # Hlavný dokument
└── README.md              # Tento súbor
```
## Použitie

### Pridávanie obsahu

Prácu môžete začať písať v časti **Document Body** súboru `main.tex`:
```tex
%%%%%%% DOCUMENT BODY %%%%%%%
\section{Úvod}
Váš text...
```

Pre lepšiu prehľadnosť rozdeľte obsah do samostatných súborov:
```tex
% %%%%%%% DOCUMENT BODY %%%%%%%
\include{chapters/introduction}
\include{chapters/implementation}
\include{chapters/summary}
```

Časť `examples` je prevažne určená univerzitou, používajte ju ako vzor.
> **Poznámka**: Vo finálnej verzii odstráňte z `main.tex` riadok `\include{examples/examples}`.

### Bibliografia
Zdroje sú uložené v `essentials/bibliography.bib` a zobrazujú sa podľa normy **STN ISO 690**. Príklady nájdete priamo v súbore.

```bibtex
@book{borgman2003from,
author = {Borgman, Christine L.},
title = {From {Gutenberg} to the Global Information Infrastructure},
subtitle = {Access to Information in the Networked World},
location = {Cambridge (Mass.)},
publisher = {The MIT Press},
date = {2003},
pagetotal = {xviii, 324},
isbn = {0-262-52345-0},
langid = {english},
}
```

Citačný štýl môžete voliteľne nastaviť v časti bibliografie v `main.tex` parametrom `style=nazov-stylu`.

Dostupné štýly sú `iso-authoryear` (predvolený) a `iso-numeric`. Viac v časti **Citovanie**.

> **Poznámka**: Po úprave bibliografie treba dokument zostaviť celým postupom (vrátane `biber`).

### Citovanie
Šablóna podporuje dva citačné štýly:

1. **Štýl autor–rok** (`iso-authoryear`)
   - `\parencite{}` vloží odkaz v zátvorkách
   - Formát: `\parencite{key}` → (Autor, Rok)
   - Príklad: `\parencite{knuth1984}` → (Knuth, 1984)
   ---
   - `\textcite{}` vloží odkaz priamo do textu
   - Formát: `\textcite{key}` → Autor, Rok
   - Príklad: `\textcite{knuth1984}` → Knuth, 1984


2. **Číselný štýl** (`iso-numeric`)
   - `\cite{}` vloží do textu číslo `[X]` a zdroje zoradí podľa poradia výskytu
   - Formát: `\cite{key}` → [1]
   - Príklad: `\cite{knuth1984}` → [1]
   

> **Poznámka**: Citačný štýl zmeníte parametrom `style` v `main.tex`:
> ```tex
> \usepackage[
>     style=iso-authoryear, % alebo iso-numeric
> ]{biblatex}
> ```

### Skratky
Skratky sú uložené v `essentials/acronyms.tex`.

#### Pridanie novej skratky
Nové skratky pridajte na koniec `essentials/acronyms.tex` podľa tohto vzoru:
```tex
\newacronym
    [description={Váš popis}]
    {label}{SKRATKA}{Celý názov}
```

Príklad:
```tex
\newacronym
    [description={Visual modeling language for software design and architecture}]
    {UML}{UML}{Unified Modeling Language}
```

#### Používanie skratiek
Skratku v texte použijete príkazom `\gls{label}`:
- **Prvé použitie zobrazí:** „Celý názov (SKRATKA)“
- **Ďalšie použitia zobrazia iba:** „SKRATKA“

Príklad:
```tex
Prvé použitie: \gls{UML} zobrazí „Unified Modeling Language (UML)“
Druhé použitie: \gls{UML} zobrazí iba „UML“
```

> **Poznámka**: Po pridaní alebo úprave skratiek treba dokument zostaviť celým postupom (vrátane `makeglossaries`).

### Obrázky

#### Predvolené nastavenie
Všetky obrázky sa automaticky centrujú a ich šírka je 90 % šírky textu.

> **Poznámka**: Predvolené nastavenie môžete zmeniť v `main.tex` v časti **Default image options**.

#### Základné použitie
Vloženie obrázka s popisom:
```tex
\begin{figure}[h]
    \includegraphics{cesta/k/obrazku}
    \caption{Váš popis}
    \label{fig:unikatny-label}
\end{figure}
```

Predvolené nastavenie môžete pre jednotlivý obrázok zmeniť argumentmi, napríklad:
```tex
\includegraphics[height=0.75\textwidth,angle=90]{image/to/rotate.png}
```
### Výpisy kódu

Nový výpis kódu so zadaným jazykom vložíte takto:
```tex
\begin{lstlisting}[language=Python, caption={Váš popis}, label={lst:python-example}]    
Váš kód...
\end{lstlisting}
```

> **Poznámka**: Predvolené nastavenie môžete zmeniť v `main.tex` v časti **Code blocks**.

## Riešenie problémov

### macOS: `biber` hlási „extracting arm64 binary with lipo failed“

Na macOS 27 zlyhá `biber` z TeX Live 2025 s chybou:
```
biber: extracting arm64 binary with lipo failed (wstatus=256)
```
Univerzálny `biber` sa pri spustení rozbaľuje príkazom `lipo -extract_family`, ktorý `/usr/bin/lipo` na macOS 27 nepodporuje. Obchádzka: vytvorte si arm64 verziu `biber` a dajte ju do PATH pred TeX Live:
```bash
mkdir -p ~/bin
lipo /usr/local/texlive/2025/bin/universal-darwin/biber -thin arm64 -output ~/bin/biber
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
```
Potom otvorte nové okno Terminálu a overte `biber --version`. Pri inom ročníku TeX Live upravte v ceste rok (`2025`).

## Licencia

Toto dielo je uvoľnené do verejnej domény pod licenciou CC0 1.0 Universal.

[![CC0](https://i.creativecommons.org/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

V rozsahu, v akom to zákon dovoľuje, sa autor vzdal všetkých autorských a súvisiacich práv k tomuto dielu.
