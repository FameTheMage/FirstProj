# AGENTS.md

Instruktioner till AI-agenter som arbetar i det här projektet.

## Projektöversikt
Enkel tvåspråkig (svenska/engelska) välkomstsida för AI-kursen med tre färgteman: mörkt, ljust och färgrikt (regnbåge).
Språkväxlare med svensk och brittisk flagga sitter uppe till höger. Temaväxlare med tre färgprickar sitter uppe till vänster.
Båda valen sparas i `localStorage` (`lang` och `theme`). Första besöket följer systemets färgschema (ljust/mörkt), annars mörkt.
Sidan är responsiv och ska fungera på mobil i både stående och liggande läge.

## Filstruktur
- `index.html` – hela sidan (HTML, CSS och JavaScript i samma fil)
- `README.md` – beskrivning för människor, på svenska och engelska
- `AGENTS.md` – den här filen
- `.gitignore` – filer som inte ska med i git

## Regler
- Använd ren HTML, CSS och JavaScript. Inga ramverk, bygg-steg eller externa beroenden utan att fråga först.
- All synlig text ska finnas på både svenska och engelska (se `translations` i `index.html`).
- Alla tre teman ska fungera. Färger styrs av CSS-variabler: mörkt i `:root`, övriga i `[data-theme="light"]` och `[data-theme="rainbow"]`. Hårdkoda inte färger i vanliga regler.
- Håll sidan tillgänglig: `lang`-attribut på `<html>`, `aria-label` och `aria-pressed` på flagg- och temaknapparna (aria-label översätts via `translations`). Säkra god kontrast i alla teman.
- Håll sidan responsiv: använd flytande enheter och media queries, knappar med minst 44 px träffyta, och testa stående och liggande mobilstorlek.
- **Kommentarer:** varje ny del (CSS-block, HTML-sektion, funktion) ska ha en kort beskrivande kommentar på svenska. Uppdatera kommentarerna när koden ändras.

## Arbetssätt
- Svara och kommunicera på svenska.
- Gör inga commits eller pushes till GitHub om användaren inte ber om det.
- Testa genom att öppna `index.html` direkt i en webbläsare.
