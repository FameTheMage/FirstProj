# AGENTS.md

Instruktioner till AI-agenter som arbetar i det här projektet.

## Projektöversikt
Enkel tvåspråkig (svenska/engelska) välkomstsida för AI-kursen. Mörkt tema.
Språkväxlare med svensk och brittisk flagga sitter uppe till höger, och valet sparas i `localStorage`.

## Filstruktur
- `index.html` – hela sidan (HTML, CSS och JavaScript i samma fil)
- `README.md` – beskrivning för människor, på svenska och engelska
- `AGENTS.md` – den här filen
- `.gitignore` – filer som inte ska med i git

## Regler
- Använd ren HTML, CSS och JavaScript. Inga ramverk, bygg-steg eller externa beroenden utan att fråga först.
- All synlig text ska finnas på både svenska och engelska (se `translations` i `index.html`).
- Behåll det mörka temat och använd färgvariablerna i `:root`.
- Håll sidan tillgänglig: `lang`-attribut på `<html>`, `aria-label` och `aria-pressed` på flaggknapparna.
- **Kommentarer:** varje ny del (CSS-block, HTML-sektion, funktion) ska ha en kort beskrivande kommentar på svenska. Uppdatera kommentarerna när koden ändras.

## Arbetssätt
- Svara och kommunicera på svenska.
- Gör inga commits eller pushes till GitHub om användaren inte ber om det.
- Testa genom att öppna `index.html` direkt i en webbläsare.
