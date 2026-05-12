# 🌐 Sito web Milestonely

Mini-versione web demo dell'app, bilingue IT/EN, brand-coerente.

**Caratteristiche:**
- Stesso look dell'app (viola brand, card eventi, banner Premium).
- Max **2 eventi** (demo limitata, spinge al download dell'app).
- Niente "Gruppi" (feature riservata all'app).
- **Niente persistenza**: i dati si azzerano ad ogni refresh (zero cookie, zero localStorage).
- **CTA download** fissa in basso, sempre visibile.
- **2 banner pubblicitari** AdSense pronti per essere attivati.
- Privacy Policy linkata in footer.
- Auto-rileva la lingua del browser (IT default, EN se browser inglese).

---

## 🖥 1. Vedi il sito in locale (subito, senza nulla da installare)

Apri Esplora File, vai in:
```
C:\Users\Utente\Documents\Claude\Projects\MILESTONELY\site\
```
Doppio click su `index.html`. Si apre nel tuo browser. Provalo, aggiungi 2 eventi finti, clicca su uno per vedere il dialog delle ricorrenze.

> Se vuoi un server locale (alcune cose si comportano meglio con un server vero), apri PowerShell nella cartella `site\` e lancia:
> ```powershell
> python -m http.server 8000
> ```
> Poi apri `http://localhost:8000` nel browser.

---

## 🌍 2. Compra il dominio `milestonely.app`

Hosting consigliato per il dominio: **Cloudflare Registrar** (≈ 8 €/anno, no markup, no rinnovi truffaldini).

1. Vai su [https://www.cloudflare.com](https://www.cloudflare.com) → registrati (gratis).
2. Menu in alto: *Domain Registration → Register Domains*.
3. Cerca `milestonely.app` → aggiungi al carrello → paga.
4. Quando il dominio è tuo, vai in *DNS* del dominio: appariranno i record DNS che configurerai al punto 4.

> Alternativa: **Namecheap** (~ 14 €/anno), **Porkbun** (~ 11 €/anno). I `.app` sono leggermente più cari dei `.com` perché obbligano HTTPS.

---

## 🚀 3. Pubblica su GitHub Pages (gratis)

Procedi come hai già fatto per la Privacy Policy.

### A. Crea un nuovo repository
1. Vai su [https://github.com/new](https://github.com/new)
2. Nome repo: `milestonely-site` (o come preferisci)
3. Visibility: **Public** (necessario per Pages gratis)
4. Spunta "Add a README"
5. Crea il repository

### B. Carica i file del sito
Su GitHub clicca *Add file → Upload files*, poi trascina dentro **tutto il contenuto** di `C:\Users\Utente\Documents\Claude\Projects\MILESTONELY\site\` (cioè `index.html`, `favicon.ico`, la cartella `img/`, e questo `README.md`).

Conferma con il bottone *Commit changes* in fondo.

### C. Attiva GitHub Pages
1. Dal repo, vai su *Settings* (tab in alto a destra).
2. Menu a sinistra → *Pages*.
3. Sotto "Build and deployment":
   - Source: **Deploy from a branch**
   - Branch: `main` / `(root)` → *Save*
4. Aspetta ~1 minuto. In cima alla pagina apparirà:
   `Your site is live at https://mjf76.github.io/milestonely-site/`

Quel link funziona già. Puoi usarlo subito.

---

## 🔗 4. Punta il dominio milestonely.app a GitHub Pages

(Solo dopo aver completato i punti 2 e 3.)

### A. Sul repo GitHub
1. *Settings → Pages → Custom domain*: scrivi `milestonely.app` → *Save*.
2. GitHub crea un file `CNAME` nel repo automaticamente.

### B. Su Cloudflare (DNS del dominio)
Apri la dashboard Cloudflare → tuo dominio → *DNS → Records*. Aggiungi questi record:

| Type | Name | Content | Proxy |
|---|---|---|---|
| A | @ | 185.199.108.153 | DNS only ☁ disattivato |
| A | @ | 185.199.109.153 | DNS only |
| A | @ | 185.199.110.153 | DNS only |
| A | @ | 185.199.111.153 | DNS only |
| CNAME | www | mjf76.github.io | DNS only |

Salva. Aspetta 10-60 minuti (a volte fino a 24h) per la propagazione DNS.

### C. Forza HTTPS
Quando GitHub vede il dominio funzionante (di solito entro 24h):
- Sul repo *Settings → Pages* → spunta **Enforce HTTPS**.

Da quel momento `https://milestonely.app` è il tuo sito ufficiale.

---

## 💰 5. Attiva AdSense (per i banner pubblicitari)

⚠️ AdSense funziona solo se hai un dominio tuo (`milestonely.app`), traffico minimo e contenuto considerato "di valore" da Google. Quindi questo passaggio si fa **dopo** che il dominio è live e l'app è pubblicata.

### A. Iscriviti
1. Vai su [https://www.google.com/adsense](https://www.google.com/adsense)
2. Login con `milestonely.app@gmail.com`
3. Aggiungi il sito `milestonely.app`
4. Inserisci dati fiscali (gli stessi del Play Console)
5. Aspetta approvazione (1-30 giorni)

### B. Una volta approvato
1. AdSense ti darà un **Publisher ID** del tipo `ca-pub-1234567890123456`.
2. Apri `index.html` con VS Code (o Blocco note).
3. Cerca `ca-pub-XXXXXXXXXXXXXX` (compare 1 volta nel commento dello script AdSense in alto). Sostituiscilo con il tuo Publisher ID reale e **decommenta** lo `<script>` (togli `<!--` e `-->`).
4. Cerca `<!-- ===== AD SLOT TOP ===== -->` e `<!-- ===== AD SLOT BOTTOM ===== -->`. In ognuno, sostituisci il `<div class="ad-slot">Annuncio</div>` con il blocco `<ins class="adsbygoogle">...</ins>` che AdSense ti fornirà per quello slot.
5. Carica le modifiche su GitHub. In 1-2 minuti i banner appaiono.

---

## 📁 Struttura cartella

```
site/
├── index.html       ← il sito (1 solo file)
├── favicon.ico      ← icona della scheda browser
├── README.md        ← questa guida
└── img/
    ├── icon.png             ← icona app 512×512
    ├── favicon.png          ← icona browser 32×32
    ├── banner_it.png        ← Open Graph IT (Facebook/WA preview)
    ├── banner_en.png        ← Open Graph EN
    └── shot1..5.png         ← non usati nel sito demo (riservati per future
                                landing/blog page se vorrai espandere)
```

---

## 🔧 Manutenzione

- **Cambio testi**: modifica direttamente l'`index.html`. Cerca i blocchi `I18N.it = {...}` e `I18N.en = {...}` per i testi tradotti.
- **Cambio colori**: in cima alla sezione `<style>` trovi tutti gli hex (`#7F77DD` ecc.).
- **Cambio CTA download**: cerca `id="play-link"`. Quando l'app sarà su Play Store, sostituisci `onclick="..."` con `href="https://play.google.com/store/apps/details?id=app.milestonely"`.
- **Disabilitare il dialog "L'app sta arrivando"**: stessa cosa, basta cambiare l'`href`.
