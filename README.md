# Adventure Cruises Malta — GitHub Pages

Questa versione mantiene il sito statico, le immagini, il layout, le animazioni, il lightbox e il modulo di prenotazione, ma è stata convertita per funzionare su GitHub Pages.

## Pubblicazione

1. Carica il contenuto di questa cartella in un repository GitHub.
2. Vai in **Settings → Pages**.
3. Seleziona **Deploy from a branch**.
4. Scegli il branch (di solito `main`) e la cartella `/ (root)`.
5. Salva e attendi il deploy.

`index.html` è già nella root del progetto e `.nojekyll` evita elaborazioni Jekyll non necessarie.

## Prenotazioni: differenza importante rispetto al PHP originale

GitHub Pages esegue solo file statici e **non può eseguire PHP**. Per questo sono stati rimossi `api/*.php`, `admin.php` e il database JSON server-side.

Il modulo ora:
- valida date, tour, orari e numero di persone;
- controlla la disponibilità delle prenotazioni salvate **nel browser corrente**;
- genera un riferimento `ACM-XXXXXXXX`;
- salva la richiesta in `localStorage`;
- apre il programma email del visitatore con una richiesta completa indirizzata a `info@adventurecruisesmalta.com`.

### Admin locale

Apri `admin.html` dallo stesso browser/dispositivo usato per effettuare le prenotazioni per vedere, modificare lo stato ed esportare le prenotazioni locali.

**Nota:** questa non è una sostituzione server-side del vecchio admin PHP. Per avere disponibilità condivisa tra tutti i visitatori, prenotazioni centralizzate e pannello admin online identico al precedente, serve un backend esterno/serverless (ad esempio Supabase, Firebase, Formspree + database, o un'API propria). GitHub Pages da solo non può fornire questa parte.

## Struttura

- `index.html` — sito completo
- `admin.html` — gestione locale delle prenotazioni del browser
- `assets/css/style.css` — CSS originale
- `assets/images/` — immagini locali
- `.nojekyll` — configurazione GitHub Pages
- `404.html` — fallback per GitHub Pages

## Nota

I link a telefono, email, Google Maps, Revolut e PayPal restano presenti come nel progetto originale.


## Fix GitHub Pages CSS/assets

Tutti i percorsi locali di CSS, JavaScript e immagini sono relativi (`assets/...`) e non iniziano con `/`.
Questo è importante quando il repository viene pubblicato come:

`https://USERNAME.github.io/NOME-REPOSITORY/`

### Pubblicazione consigliata

1. Crea un repository GitHub.
2. Carica **il contenuto dello ZIP**, non la cartella ZIP stessa.
3. Verifica che `index.html` sia nella root del repository.
4. In **Settings → Pages**, puoi usare **GitHub Actions**; il workflow incluso (`.github/workflows/pages.yml`) effettua il deploy automaticamente quando fai push su `main`.
5. Se preferisci "Deploy from a branch", scegli `main` e `/ (root)`.

Non aprire `index.html` con un percorso file locale per verificare GitHub Pages: usa l'URL Pages del repository.
