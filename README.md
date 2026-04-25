# Wine Guide — Guida al deploy su Netlify + sottodominio

## Cosa contiene questa cartella

- `index.html` — la landing page completa (quiz + matching + raccolta email)
- `netlify.toml` — configurazione automatica per Netlify
- `README.md` — questa guida

---

## STEP 1 — Crea un account Netlify (gratis)

1. Vai su https://netlify.com
2. Clicca "Sign up" → registrati con email o GitHub
3. Conferma l'email

---

## STEP 2 — Pubblica il sito su Netlify

### Metodo più semplice: drag & drop

1. Vai su https://app.netlify.com
2. Nella home, cerca la sezione **"Deploy manually"** o **"Sites"**
3. Trascina l'intera cartella `wine-guide-site` nella finestra del browser
4. Netlify pubblica il sito in 30 secondi
5. Ti assegna un URL temporaneo tipo: `https://amazing-wine-123.netlify.app`
   → Aprilo per verificare che tutto funzioni

---

## STEP 3 — Configura il sottodominio su Netlify

1. Nel pannello del tuo sito su Netlify, vai su **Site configuration → Domain management**
2. Clicca **"Add a domain"**
3. Inserisci il sottodominio che vuoi usare, ad esempio:
   `guida.tuosito.com`
4. Netlify ti mostrerà un valore CNAME da copiare — tienilo aperto

---

## STEP 4 — Configura il DNS su Squarespace

1. Accedi a Squarespace → **Settings → Domains**
2. Clicca sul tuo dominio principale
3. Vai su **DNS Settings** (in basso nella pagina)
4. Clicca **"Add record"** e inserisci:

   | Tipo   | Host   | Valore                          |
   |--------|--------|---------------------------------|
   | CNAME  | guida  | [il valore che ti ha dato Netlify] |

   Esempio:
   | CNAME  | guida  | amazing-wine-123.netlify.app    |

5. Salva

> ⏱ La propagazione DNS richiede da 5 minuti a 24 ore.
> Netlify attiva automaticamente HTTPS (certificato SSL gratuito).

---

## STEP 5 — Collega il dominio su Netlify

1. Torna su Netlify → Domain management
2. Clicca **"Verify"** accanto al sottodominio
3. Quando la propagazione è completata, Netlify lo segna come attivo ✓
4. Il tuo sito sarà live su `https://guida.tuosito.com`

---

## Come aggiornare le guide in futuro

Apri `index.html` con un editor di testo (anche il Blocco Note va bene).
Cerca la sezione `const GUIDES_DB = [` — da lì puoi:

- **Aggiungere una guida**: copia un blocco esistente e modifica i campi
- **Modificare una guida**: cambia titolo, descrizione, tag o punteggi di match
- **Rimuovere una guida**: elimina il blocco corrispondente

Dopo ogni modifica, torna su Netlify e trascina di nuovo la cartella
nella sezione "Deploys" → il sito si aggiorna in pochi secondi.

### Struttura di una guida nel database

```javascript
{
  id: "id-unico",               // identificatore interno
  title: "Titolo della guida",
  desc: "Descrizione breve.",
  tags: ["tag1", "tag2"],       // etichette visibili sulla card
  match: {                      // punteggio 0-100 per ogni livello utente
    curioso: 80,
    appassionato: 90,
    intenditore: 60,
    esperto: 40
  },
  focus: ["scoperta"],          // scoperta | abbinamento | degustazione | territorio
  occasion: ["quotidiano"]      // quotidiano | speciale | formazione | viaggio
}
```

---

## Collegare la Google My Map

Apri `index.html`, cerca questa riga:

```javascript
const MAP_URL = 'https://www.google.com/maps/d/YOUR_MAP_ID';
```

Sostituisci `YOUR_MAP_ID` con l'ID della tua Google My Map.
Lo trovi nell'URL della mappa quando la apri:
`https://www.google.com/maps/d/edit?mid=QUESTO_E_IL_TUO_ID`

---

## Prossimi step (quando sei pronto)

1. **Connettere un servizio email** (Mailchimp, ConvertKit, ecc.)
   per raccogliere davvero le email degli iscritti
2. **Spostare il database su Google Sheets o Airtable**
   per aggiornare le guide senza toccare il codice
3. **Aggiungere il wine coach AI**
   che risponde attingendo al tuo catalogo curato
