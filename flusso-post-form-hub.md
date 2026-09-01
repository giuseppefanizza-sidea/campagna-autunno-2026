# Flusso post-form Hub — Campagna "AI che lavora"

> Autunno 2026 · Sidea Group

---

## Obiettivo

Dopo la compilazione del form sulla pagina Hub (`/hub/#contattaci`), il lead riceve immediatamente un'email con:

1. Conferma della ricezione della richiesta
2. Link alle 5 demo tematiche da guardare in attesa della chiamata
3. Aspettativa chiara: un consulente Sidea chiamerà a breve per individuare le esigenze specifiche del progetto

---

## Trigger

| Evento | Dettaglio |
|--------|-----------|
| Form submit | Form "Racconta il tuo problema" su `/hub/#contattaci` |
| Campi raccolti | soluzione (select), nome, cognome, email, telefono, azienda, ruolo, esigenza (textarea) |

---

## Azioni del flusso

### Step 1 — Email immediata (delay: 0 min)

**A:** `{{email}}`  
**Da:** Sidea Group <noreply@sideagroup.com>  
**Oggetto:** Grazie {{nome}} — ecco le 5 soluzioni AI da esplorare  
**Template:** `email-hub-followup/index.html`

Contenuto:
- Ringraziamento per la richiesta
- Riepilogo breve delle 5 soluzioni con link diretto alla demo tematica
- Messaggio: "Un consulente Sidea ti chiamerà a breve per individuare insieme le esigenze specifiche del tuo progetto"
- CTA secondaria: se vuole anticipare, può rispondere a questa email

### Step 2 — Notifica interna al BDR (delay: 0 min)

**A:** Team BDR (canale Slack / email interna)  
**Contenuto:**
- Nome, cognome, azienda, ruolo
- Soluzione selezionata (o "Non so ancora")
- Testo dell'esigenza
- Link al record CRM (se integrato)

### Step 3 — Reminder al BDR (delay: 24h)

Se il lead non è stato contattato (status CRM ≠ "contacted"):
- Reminder interno al BDR assegnato
- Escalation al sales manager se > 48h

---

## Segmentazione futura (opzionale)

Se il campo `soluzione` è valorizzato con una scelta specifica, il flusso può:
- Evidenziare quella soluzione in cima alla lista nell'email
- Assegnare il BDR di competenza verticale
- Taggare il lead nel CRM con l'interesse specifico

---

## Asset collegati

| Asset | Path |
|-------|------|
| Email follow-up hub | `email-hub-followup/index.html` |
| Demo BEA | `/demo-bea/` |
| Demo Dynamic Pricing | `/demo-pricing/` |
| Demo Forecasting | `/demo-forecasting/` |
| Demo Patient Intake (Lucea) | `/demo-lucea/` |
| Demo Content Generator | `/demo-content/` |

---

## Note implementative

- L'email deve funzionare su tutti i client (Outlook, Gmail, Apple Mail) — struttura table-based
- I link alle demo usano URL assoluti: `https://giuseppefanizza-sidea.github.io/campagna-autunno-2026/demo-{slug}/`
- Il template segue lo stesso design system delle email esistenti (`email-bea/`, `email-pricing/`, ecc.)
- Personalizzazione con merge tag `{{nome}}`
