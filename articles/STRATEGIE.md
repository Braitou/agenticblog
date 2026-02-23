# Stratégie Éditoriale — Agentic Flow Blog

## Objectif

Générer du trafic organique qualifié (marchands Shopify) via le blog, et les convertir vers l'app Agentic Flow sur le Shopify App Store.

Funnel : **Article SEO → Lecture → CTA → Shopify App Store → Installation**

## Calendrier de publication

**Rythme : 2 articles par semaine** (ex : mardi + jeudi)

### Articles prêts (à publier)

| # | Fichier | Titre | Publication suggérée |
|---|---------|-------|---------------------|
| 1 | `google-ai-overviews-shopify.md` | Google AI Overviews: How to Get Your Shopify Products Featured | Semaine 1 - Jour 1 |
| 2 | `indexnow-shopify-guide.md` | IndexNow for Shopify: The Complete Guide to Instant Search Engine Notification | Semaine 1 - Jour 2 |
| 3 | `schema-json-ld-shopify-products.md` | Schema.org JSON-LD for Shopify Products: What AI Engines Actually Want to See | Semaine 2 - Jour 1 |
| 4 | `perplexity-shopping-ecommerce.md` | Perplexity Shopping: What E-Commerce Merchants Need to Know | Semaine 2 - Jour 2 |

### Pour publier un article

1. Copier le fichier `.md` depuis `articles/` vers `src/content/blog/`
2. Mettre à jour le champ `pubDate` dans le frontmatter avec la date du jour
3. Commit + push sur `main` → le déploiement GitHub Actions se lance automatiquement

## Sujets futurs (backlog)

- Shopify Agentic Storefronts : la prochaine révolution du commerce AI
- robots.txt pour Shopify : faut-il bloquer les crawlers AI ?
- GTIN, EAN, UPC : pourquoi c'est devenu obligatoire pour le SEO produit
- Comment auditer le JSON-LD de votre boutique Shopify
- E-E-A-T pour les pages produit : ce que Google attend vraiment
- Les meilleures apps Shopify pour le SEO en 2026
- Microsoft Copilot Shopping : un canal sous-estimé
- Avant/Après : résultats réels d'optimisation AEO sur Shopify

## Règles de ton et style

- **Honnête et data-backed** : chaque affirmation doit être sourcée ou vérifiable
- **Pas de hype** : ne jamais promettre de résultats garantis
- **Sceptique constructif** : questionner les narratifs de l'industrie avec des données
- **Technique mais accessible** : expliquer JSON-LD, IndexNow, GTINs en langage clair
- **Conversationnel** : première personne ("we built", "we looked at the data")
- **Orienté action** : chaque section doit inclure des étapes concrètes

## Intégration des CTA

- Le CTA vers l'app arrive **toujours après** avoir apporté de la valeur
- Mentionner le **tier gratuit** (20 produits) pour réduire la friction
- Ajouter une phrase qualifiante ("But regardless of what tool you use...")
- URL de l'app : `https://apps.shopify.com/agentic-flow-aeo-metafields`
- Cross-links vers les autres articles du blog en fin d'article

## KPIs à suivre

### Google Search Console (priorité #1)
- Impressions par article
- Clics organiques par article
- Position moyenne par mot-clé
- Taux de clic (CTR) par article
- Soumettre le sitemap : `https://agentic-flow.app/sitemap-index.xml`

### Google Analytics / Plausible (priorité #2)
- Trafic par article (sessions, users)
- Taux de rebond par article
- Clics sur les CTA vers le Shopify App Store (event tracking)
- Parcours : article → about → app store

### Shopify Partner Dashboard
- Sources de trafic vers la page app
- Installations attribuées au blog (si trackable)

## Mots-clés cibles par article

| Article | Mots-clés primaires |
|---------|-------------------|
| Google AI Overviews | google ai overviews shopify, ai overviews e-commerce, google sge products |
| IndexNow | indexnow shopify, indexnow tutorial, notify search engines shopify |
| JSON-LD | json-ld shopify, schema.org shopify products, structured data shopify |
| Perplexity Shopping | perplexity shopping, perplexity e-commerce, perplexity product recommendations |
| (existant) AEO Guide | what is aeo, answer engine optimization shopify |
| (existant) ChatGPT | shopify chatgpt recommendations, chatgpt product search |
| (existant) llms.txt | llms.txt shopify, llms.txt does it work |
