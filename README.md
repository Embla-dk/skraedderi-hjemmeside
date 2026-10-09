# Skrædderi – hjemmeside

Statisk markedsføringsside for Skrædderi-appen. Ingen build-step; Netlify udgiver mappen som den er.

```bash
python3 -m http.server 8080   # se siden lokalt på http://localhost:8080
```

## Pladsholdere, der skal rettes før lancering

| Pladsholder | Hvor |
|---|---|
| `skraedderi.dk` (domæne) | alle .html-filer, robots.txt, sitemap.xml, llms.txt |
| `app.skraedderi.dk` / `app.skraedderi.dk/signup` | knapper "Prøv gratis" og "Log ind" |
| `hej@skraedderi.dk` | footer, privatliv.html, llms.txt, JSON-LD |
| `249` kr./md. | index.html (prissektion, FAQ, JSON-LD) og llms.txt |

Ret alt på én gang, fx:

```bash
grep -rl 'skraedderi.dk' --include='*.html' --include='*.txt' --include='*.xml' . \
  | xargs sed -i 's/skraedderi\.dk/ditdomæne.dk/g'
```

Mangler også: firmanavn og CVR-nr. i footeren (e-handelsloven kræver det).

## SEO og AI-synlighed

- Titel, beskrivelse, canonical og Open Graph-billede (`og-image.png`) på hver side
- Strukturerede data (JSON-LD): Organization, WebSite, SoftwareApplication med pris, FAQPage
- `robots.txt` tillader eksplicit AI-crawlere (GPTBot, ClaudeBot, PerplexityBot m.fl.)
- `llms.txt`: kort faktaark om produktet til AI-assistenter
- `sitemap.xml`: opdatér `lastmod`, når indholdet ændres
- Skrifttyper ligger lokalt i `fonts/` (hurtigere og intet kald til Google = ingen cookie-banner nødvendig)

FAQ'en findes to steder: i HTML og i JSON-LD øverst i `index.html`. Ret begge.

Efter lancering: tilføj domænet i Google Search Console og Bing Webmaster Tools og indsend sitemap'et.
