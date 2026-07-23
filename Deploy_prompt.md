# Deploy til Simply.com & App Udviklings Prompt

Kopiér teksten herunder og indsæt den i en ny AI Studio chat, når du opretter eller vil have hjælp til at udvikle og deploye en app til Simply.com.

---

Hjælp mig med at udvikle denne app og opsætte automatisk deploy fra GitHub til Simply.com.

Her er specifikationerne og retningslinjerne for min opsætning og appen:

1.  **Database**: 
    *   **Vigtigt**: Spørg mig altid som det første, om der skal oprettes en database til denne app (f.eks. via Firebase Firestore, som vi har gjort på andre projekter). spring punktet over, hvis der er oprettet en database.

2.  **Responsivt Design & Enhedsoptimering**:
    *   Appen skal altid være fuldt optimeret til visning i browseren på både **PC, tablets (iPad) og mobile enheder**. Der må meget gerne laves forskellige opsætninger/layouts alt efter skærmstørrelsen.
    *   **Mobil-visninger**: Skal være optimeret specifikt mod nem **indtastning af data** eller ubesværet **læsning af udvalgte tekster** (større trykflader, fokuserede formularer, høj læsbarhed).

3.  **Fanebladstitel (Browser Tab Title)**:
    *   **Handling**: Spørg mig altid om, hvilket navn der skal bruges på browserens faneblad (f.eks. i `<title>` i `index.html`), og opdater det i projektet.

4.  **GitHub Action til Deploy**: 
    *   Opret en `.github/workflows/deploy.yml` fil, der installerer afhængigheder, kører `npm run build` og derefter uploader `dist/` mappen via FTP (brug f.eks. `SamKirkland/FTP-Deploy-Action`).
  
    *   [DEPLOYMENT & FTP RETNINGSLINJER]
Når du opretter GitHub Actions workflowet (.github/workflows/deploy.yml) til Simply.com:
1. Brug altid præcise versionsnumre på tredjeparts-actions (f.eks. SamKirkland/FTP-Deploy-Action@v4.3.5 i stedet for @v4).
2. Brug `npm install` i stedet for `npm ci` i installationstrinnet for at undgå fejl med manglende låsefiler.
3. Sæt `node-version: '22'` (eller nyere) under `actions/setup-node@v4` og undlad `cache: 'npm'` hvis der ikke er en fast `package-lock.json`.
4. Inkluder en sikkerhedsmargin for FTP-upload ved at tilføje `timeout: 60000` under FTP-deploy actionens `with:` blok for at undgå ECONNRESET ved første store synkronisering.
5. Sørg for at spørge om subdomænenavn og mappe (f.eks. ../subdomænenavn/) før oprettelse.

5.  **Server-struktur (Simply.com)**:
    *   Domænet er **kastanievej7.dk**.
    *   Alle apps ligger som subdomæner (f.eks. `appnavn.kastanievej7.dk`).
    *   **Vigtigt**: Mapperne til subdomænerne på webserveren ligger på samme niveau som `public_html` mappen (ikke indeni den).
    *   **Handling**: Spørg mig altid om navnet på mappen til subdomænet, før du skriver den endelige sti i workflow-filen.

6.  **GitHub Secrets**: Konfigurér workflowet til at bruge følgende 3 secrets:
    *   `FTP_SERVER`
    *   `FTP_USERNAME`
    *   `FTP_PASSWORD`

7.  **Verificering**: Tjek `package.json` for at sikre, at `npm run build` producerer en `dist/` mappe.

**Efter du har oprettet workflow-filen, skal du huske mig på følgende:**
*   At jeg manuelt skal oprette subdomænet på Simply.com (DNS/Webhotel).
*   At jeg skal oprette de 3 secrets (`FTP_SERVER`, `FTP_USERNAME`, `FTP_PASSWORD`) under 'Settings' -> 'Secrets and variables' -> 'Actions' i mit GitHub repository.
*   Bekræft hvilken sti du har brugt til `server-dir`.
