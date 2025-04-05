# Plan Implementacji Strony Huddle Landing Page

1.  **Analiza Projektu Graficznego:** Dokładnie przeanalizuję pliki w katalogu `design/` (`desktop-design.jpg`, `mobile-design.jpg`, `active-states.jpg`), aby zrozumieć układ, komponenty i wymagane interakcje.
2.  **Struktura HTML (`index.html`):**
    - Zdefiniuję semantyczną strukturę dokumentu HTML.
    - Zastosuję metodologię BEM (Block, Element, Modifier) do nazewnictwa klas CSS, aby zapewnić spójność i łatwość w utrzymaniu stylów.
3.  **Organizacja SCSS (Wzorzec 7-1):**
    - Utworzę katalog `scss/` w głównym katalogu projektu.
    - Wewnątrz `scss/` stworzę podkatalogi zgodnie ze wzorcem 7-1:
      - `abstracts/`: Będzie zawierać pliki ze zmiennymi (kolory, fonty z `style-guide.md`), mixinami i funkcjami. Np. `_variables.scss`, `_mixins.scss`.
      - `base/`: Podstawowe style dla elementów HTML, resetowanie stylów przeglądarki, definicje typografii. Np. `_reset.scss`, `_typography.scss`, `_base.scss`.
      - `components/`: Style dla reużywalnych komponentów interfejsu, takich jak przyciski, logo, ikony społecznościowe. Np. `_button.scss`, `_logo.scss`, `_social-icons.scss`.
      - `layout/`: Style definiujące główne sekcje strony, takie jak nagłówek, stopka, siatka (jeśli potrzebna). Np. `_header.scss`, `_footer.scss`, `_main-content.scss`.
      - `pages/`: Style specyficzne dla tej konkretnej strony (landing page). Np. `_home.scss`.
    - Utworzę główny plik `scss/main.scss`, który będzie importował wszystkie częściowe pliki (`_*.scss`) w odpowiedniej kolejności.
4.  **Implementacja Stylów SCSS:**
    - Napiszę style SCSS dla każdego komponentu i sekcji layoutu, korzystając ze zdefiniowanych zmiennych i mixinów.
    - Zaimplementuję responsywność, używając media queries, aby strona wyglądała dobrze na urządzeniach mobilnych (zgodnie z `mobile-design.jpg`) i desktopowych (`desktop-design.jpg`). Szczególną uwagę zwrócę na punkty przełamania (breakpoints) sugerowane w `style-guide.md` (375px, 1440px), ale zapewnię płynne przejścia.
    - Dodam style dla stanów aktywnych (np. `:hover` dla przycisków i ikon) zgodnie z `active-states.jpg`.
    - Zintegruję ikony społecznościowe, prawdopodobnie używając biblioteki Font Awesome, jak sugerowano w `style-guide.md`.
5.  **Kompilacja SCSS:** Skonfiguruję proces kompilacji SCSS do CSS (np. za pomocą rozszerzenia VS Code Live Sass Compiler lub narzędzia budującego jak Gulp/Webpack, jeśli projekt będzie rozwijany). Wynikowy plik `style.css` zostanie umieszczony w odpowiednim miejscu (np. w katalogu `css/`) i podlinkowany w `index.html`.
6.  **Weryfikacja:** Przetestuję stronę na różnych przeglądarkach i rozmiarach ekranu, aby upewnić się, że jest zgodna z projektem graficznym i w pełni responsywna.

## Wizualizacja Struktury SCSS (Mermaid)

```mermaid
graph TD
    subgraph Project Root
        direction LR
        index[index.html]
        scssDir[scss/]
        cssDir[css/]
        imgDir[images/]
        designDir[design/]
    end

    subgraph scss/ (7-1 Pattern)
        direction TB
        main[main.scss] --> abstracts(abstracts/)
        main --> base(base/)
        main --> components(components/)
        main --> layout(layout/)
        main --> pages(pages/)

        subgraph abstracts
            direction TB
            vars[_variables.scss]
            mixins[_mixins.scss]
        end

        subgraph base
            direction TB
            reset[_reset.scss]
            typo[_typography.scss]
            baseStyles[_base.scss]
        end

        subgraph components
            direction TB
            button[_button.scss]
            logo[_logo.scss]
            social[_social-icons.scss]
        end

        subgraph layout
            direction TB
            header[_header.scss]
            footer[_footer.scss]
            content[_main-content.scss]
        end

        subgraph pages
            direction TB
            home[_home.scss]
        end
    end

    scssDir --> main
    main --> cssDir -- Kompilacja --> style[style.css]
    index -- Linkuje --> style
```
