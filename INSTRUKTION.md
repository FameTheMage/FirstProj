# Instruktion: från lokal mapp till publicerad sida på GitHub Pages

Alla kommandon körs i **PowerShell** (eller Git Bash) i projektmappen.
Byt ut `DITT-ANVÄNDARNAMN` och `DITT-REPO` mot dina egna värden.

---

## Steg 0. Förberedelser

**Varför:** Git måste vara installerat och veta vem du är, annars kan du inte göra commits. Du behöver också ett GitHub-konto.

1. Skapa ett konto på https://github.com om du inte har ett.
2. Kontrollera att git finns:
   ```powershell
   git --version
   ```
3. Ange ditt namn och din e-post (görs en gång per dator):
   ```powershell
   git config --global user.name "Ditt Namn"
   git config --global user.email "din@epost.se"
   ```

**Se resultatet:** `git config --global --list` visar `user.name` och `user.email`.

---

## Steg 1. Öppna projektmappen i terminalen

**Varför:** git-kommandon gäller den mapp du står i.

```powershell
cd E:\AIKurs\FirstProj
```

**Se resultatet:** `dir` (eller `ls`) listar `index.html`, `AGENTS.md`, `README.md`, `.gitignore` och `INSTRUKTION.md`.

---

## Steg 2. Skapa ett lokalt git-repo

**Varför:** `git init` gör mappen till ett repo, så att git kan spåra ändringar. `-b main` döper huvudgrenen till `main`.

> Jag har redan kört detta åt dig. Vill du göra det själv från början, ta först bort det gamla repot (tar bara bort historiken, inte dina filer):
> ```powershell
> Remove-Item -Recurse -Force .git
> ```

```powershell
git init -b main
```

**Se resultatet:**
- Meddelandet `Initialized empty Git repository`.
- En dold mapp `.git` finns nu: `dir -Force`. Där lagrar git all historik.

---

## Steg 3. Se vad git ser

**Varför:** `git status` är det kommando du kör oftast. Det visar vilka filer som är nya, ändrade eller redo att sparas.

```powershell
git status
```

**Se resultatet:** under `Untracked files` (röda) står alla dina filer. De är ännu inte spårade av git.

---

## Steg 4. Lägg filerna i "staging"

**Varför:** Du väljer själv vilka ändringar som ska ingå i nästa commit. `git add` flyttar dem till staging-området. Punkten betyder "allt i mappen".

```powershell
git add .
git status
```

**Se resultatet:** filerna står nu under `Changes to be committed` (gröna).

---

## Steg 5. Gör din första commit

**Varför:** En commit är en sparad ögonblicksbild av projektet med ett meddelande som förklarar vad som ändrats. Du kan alltid gå tillbaka till den.

```powershell
git commit -m "Första version av AI-kursens välkomstsida"
```

**Se resultatet:**
```powershell
git log --oneline
```
Du ser din commit med ett kort id och ditt meddelande. `git status` säger nu `nothing to commit, working tree clean`.

---

## Steg 6. Skapa ett tomt repo på GitHub

**Varför:** GitHub är den fjärrplats (remote) där koden delas och där sidan publiceras.

1. Logga in på https://github.com och klicka på **+** uppe till höger, sedan **New repository**.
2. **Repository name:** t.ex. `ai-kursen`.
3. Välj **Public**. GitHub Pages är gratis för publika repon.
4. **Lämna alla rutor under "Initialize this repository" tomma** (ingen README, ingen .gitignore, ingen licens). Du har redan egna filer, och extra filer ger konflikt vid första push.
5. Klicka **Create repository**.

**Se resultatet:** GitHub visar en sida med "Quick setup" och en adress som `https://github.com/DITT-ANVÄNDARNAMN/ai-kursen.git`.

---

## Steg 7. Koppla det lokala repot till GitHub

**Varför:** Du talar om för git var fjärrrepot finns. Namnet `origin` är standardnamnet för det.

```powershell
git remote add origin https://github.com/DITT-ANVÄNDARNAMN/DITT-REPO.git
```

**Se resultatet:**
```powershell
git remote -v
```
Du ser `origin` med din adress, två rader (fetch och push).

---

## Steg 8. Skicka upp koden (push)

**Varför:** `git push` kopierar dina commits till GitHub. `-u` kopplar din lokala `main` till `origin/main`, så att du i fortsättningen bara behöver skriva `git push`.

```powershell
git push -u origin main
```

Första gången öppnas ett inloggningsfönster i webbläsaren (Git Credential Manager). Logga in på GitHub och godkänn.

**Se resultatet:** ladda om repo-sidan på GitHub. Dina filer och din commit syns där. Under **Commits** ser du historiken.

---

## Steg 9. Jobba med en branch

**Varför:** En branch är en egen arbetsgren. Du kan testa ändringar utan att röra `main`, som alltid ska vara fungerande kod. Det är så man arbetar i team.

1. Skapa och byt till en ny gren:
   ```powershell
   git switch -c feature/ny-text
   ```
2. Ändra något, t.ex. undertexten i `index.html` (både svenska och engelska).
3. Se vad som ändrats och spara:
   ```powershell
   git status
   git diff
   git add index.html
   git commit -m "Ändra undertext på startsidan"
   ```
4. Skicka upp grenen:
   ```powershell
   git push -u origin feature/ny-text
   ```

**Se resultatet:**
- `git branch` visar alla lokala grenar, och en `*` markerar den aktiva.
- `git diff` visar exakt vilka rader du ändrat (`-` borttaget, `+` tillagt).
- På GitHub: knappen **main** (grenväljaren) listar nu även `feature/ny-text`, och en gul ruta med **Compare & pull request** dyker upp.

---

## Steg 10. Pull request och merge

**Varför:** En pull request (PR) är en begäran om att slå ihop din gren med `main`. Där kan ändringarna granskas innan de blir en del av huvudkoden.

1. På GitHub, klicka **Compare & pull request**.
2. Skriv en titel och en kort beskrivning, klicka **Create pull request**.
3. Under fliken **Files changed** ser du ändringarna rad för rad.
4. Klicka **Merge pull request**, sedan **Confirm merge**.
5. Klicka **Delete branch** på GitHub (grenen behövs inte längre).

Uppdatera sedan din lokala dator:
```powershell
git switch main
git pull
git branch -d feature/ny-text
```

**Varför:** `git pull` hämtar den sammanslagna `main` från GitHub, och `git branch -d` städar bort den lokala grenen.

**Se resultatet:** `git log --oneline` visar nu båda dina commits på `main`, och `index.html` har din ändring.

---

## Steg 11. Publicera på GitHub Pages

**Varför:** GitHub Pages gör om filerna i ditt repo till en riktig webbsida på internet, gratis. Eftersom `index.html` ligger i rotmappen hittas den automatiskt.

1. Gå till ditt repo på GitHub, fliken **Settings**.
2. Klicka **Pages** i menyn till vänster.
3. Under **Build and deployment**, **Source**: välj **Deploy from a branch**.
4. Under **Branch**: välj `main` och mappen `/ (root)`, klicka **Save**.

**Se resultatet:**
- Fliken **Actions** visar en körning som heter *pages build and deployment*. Vänta tills den är grön (cirka 1 till 2 minuter).
- Gå tillbaka till **Settings, Pages**. En ruta visar **Your site is live at** och adressen:
  ```
  https://DITT-ANVÄNDARNAMN.github.io/DITT-REPO/
  ```

---

## Steg 12. Se sidan i webbläsare och på mobil

**Varför:** Du vill verifiera att den publicerade sidan fungerar, inte bara filen på din dator.

1. **Dator:** öppna adressen från steg 11 i valfri webbläsare. Klicka på flaggorna och kontrollera att språket byts.
2. **Mobil:** skriv samma adress i mobilens webbläsare. Du behöver inte vara på samma wifi, eftersom sidan ligger på internet. Du kan också skapa en QR-kod av adressen (t.ex. med en gratis QR-generator) och skanna den med kameran.
3. **Språkvalet sparas:** byt språk, ladda om sidan och kontrollera att valet finns kvar.

Om du inte ser dina senaste ändringar, tvinga omladdning med **Ctrl + F5** (på mobil: stäng fliken och öppna igen).

---

## Steg 13. Så uppdaterar du sidan framöver

**Varför:** Det här är det vanliga arbetsflödet, och det upprepar stegen ovan.

```powershell
git switch main
git pull
git switch -c feature/min-ändring
# ... ändra filer ...
git add .
git commit -m "Beskriv ändringen"
git push -u origin feature/min-ändring
```
Skapa sedan en pull request, merga den på GitHub, och kör `git switch main` och `git pull`. GitHub Pages publicerar om automatiskt efter någon minut.

---

## Vanliga problem

| Problem | Orsak och lösning |
|---|---|
| `Author identity unknown` vid commit | Steg 0 saknas: kör `git config --global user.name` och `user.email`. |
| `rejected ... fetch first` vid push | Du skapade GitHub-repot med en README. Kör `git pull origin main --allow-unrelated-histories` och sedan `git push`. |
| `remote origin already exists` | Byt adress med `git remote set-url origin NY-ADRESS`. |
| 404 på sidan | Pages är inte klart ännu (vänta), eller så pekar Source inte på `main` och `/ (root)`. |
| Gamla ändringar syns | Webbläsaren cachar. Tryck Ctrl + F5. |

## Snabbreferens

| Kommando | Gör |
|---|---|
| `git status` | Visar läget just nu |
| `git diff` | Visar ändringar rad för rad |
| `git add .` | Förbereder alla ändringar för commit |
| `git commit -m "text"` | Sparar en commit |
| `git log --oneline` | Visar historiken kort |
| `git branch` | Listar grenar |
| `git switch NAMN` | Byter gren |
| `git switch -c NAMN` | Skapar och byter till ny gren |
| `git push` | Skickar upp commits |
| `git pull` | Hämtar ner ändringar |
