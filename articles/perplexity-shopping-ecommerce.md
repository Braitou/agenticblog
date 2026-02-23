---
title: 'Perplexity Shopping: What E-Commerce Merchants Need to Know'
description: 'Perplexity is becoming a product discovery engine. Here is how it finds and recommends products, and what Shopify merchants can do about it.'
pubDate: 2026-03-05
---

There is a good chance your customers are already using Perplexity to find products. Not to search for your brand name -- but to ask questions like "best waterproof hiking boots under $200" or "lightweight stroller for travel." And when they do, Perplexity doesn't just give them a list of links. It gives them product cards with images, prices, reviews, and buy buttons.

Most Shopify merchants we talk to have heard of ChatGPT Shopping. Some are aware of Google AI Overviews. Almost none have Perplexity on their radar. That's a mistake, because Perplexity is building one of the most aggressive AI-powered shopping experiences on the web right now -- and it works differently from everything else.

## What Is Perplexity, and Why Should Merchants Care?

Perplexity is an AI-powered answer engine. Unlike ChatGPT, which started as a conversational assistant and bolted on search later, Perplexity was built from day one to search the web, synthesize information, and cite its sources. It launched its dedicated shopping experience in late 2024 and has been expanding it aggressively since.

The key difference from ChatGPT for product discovery:

- **Perplexity always searches the live web.** ChatGPT can search the web (via Bing), but it also draws heavily on its training data. Perplexity queries real-time sources for every answer. This means fresh product data, current pricing, and up-to-date availability matter more on Perplexity than on ChatGPT.
- **Perplexity cites its sources with links.** Every product recommendation includes a clickable source. This is closer to a traditional search result than ChatGPT's recommendation style, where attribution is often buried or absent.
- **Perplexity has a dedicated shopping UI.** Product cards with images, prices, merchant names, and direct purchase links. This is not a chatbot that happens to mention products -- it is a product discovery interface.

As of early 2026, Perplexity reports over 100 million monthly queries and has raised over $500 million in funding. Their Pro tier has over 1 million subscribers. The numbers are smaller than ChatGPT, but the intent signal is strong: people using Perplexity for product queries are actively shopping.

## How Perplexity Actually Finds Products

This is where it gets practical. We dug into how Perplexity discovers and surfaces products, because knowing the plumbing matters more than knowing the marketing pitch.

**1. Web crawling and indexing.** Perplexity operates its own web crawler (PerplexityBot). It crawls product pages directly and builds its own index. This is fundamentally different from ChatGPT, which relies on Bing's index. If PerplexityBot can access your product pages, Perplexity can find your products.

**2. Third-party search indexes.** Perplexity also pulls from Bing and Google search results as supplementary sources. So even if PerplexityBot hasn't crawled your site directly, your products can appear via these secondary indexes.

**3. Structured data on your pages.** When PerplexityBot crawls a product page, it reads Schema.org JSON-LD markup -- the same structured data that Google and Bing use. Product name, price, availability, GTIN, reviews, brand, images. The richer your structured data, the more information Perplexity has to build product cards.

**4. Merchant data partnerships.** Perplexity has been building direct merchant integrations, particularly with Shopify. Shopify's [Agentic Storefronts](https://www.shopify.com/news/agentic-commerce) initiative syndicates product catalog data directly to AI engines including Perplexity. If you are on Shopify, some of your product data may already be flowing to Perplexity through this channel.

**What to do:** Check your robots.txt right now. Go to `yourstore.com/robots.txt` and make sure you are NOT blocking `PerplexityBot`. If you see a `Disallow` directive for PerplexityBot, remove it. You want Perplexity's crawler to access your product pages.

## Perplexity Shopping Features

Perplexity's shopping experience has matured significantly. Here is what it looks like in practice:

- **Product cards.** When a user asks a shopping question, Perplexity displays visual product cards with images, product names, prices, merchant names, and star ratings. These are not just text mentions -- they are rich, clickable cards.
- **Price comparisons.** Perplexity aggregates pricing from multiple retailers for the same product (matched by GTIN). If you sell a product that five other retailers also carry, Perplexity can show your price alongside theirs.
- **Direct purchase links.** Each product card links directly to the merchant's product page. Perplexity Pro users can also use "Buy with Pro," a one-click checkout feature powered by Perplexity's own payment infrastructure.
- **Product snapshots.** Perplexity generates AI-written product summaries that synthesize reviews, specifications, and merchant descriptions into a quick overview.
- **Follow-up refinement.** Users can refine their search conversationally: "Show me only the ones with free shipping" or "Which of these has the best reviews?" Perplexity filters its product results in real time.

**What to do:** Search for one of your own products on Perplexity (perplexity.ai). Try both the product name and a generic query that should surface it (e.g., "best [category] under $[price]"). See what shows up. If your product appears, check whether the card has accurate pricing, a good image, and correct availability. If it doesn't appear, you now know what to fix.

## What Actually Helps Your Products Appear in Perplexity

Based on what we know about Perplexity's architecture, here is what genuinely moves the needle:

### Rich structured data (JSON-LD) -- High impact

This is the single most important factor, and it is the same foundation that works for [ChatGPT recommendations](/blog/shopify-products-chatgpt-recommendations/) and Google AI Overviews. A comprehensive Schema.org Product JSON-LD block gives Perplexity everything it needs to build a product card: name, image, price, availability, brand, GTIN, reviews, category, color, material.

Most Shopify themes include bare-minimum JSON-LD. The fields that Perplexity Shopping actually uses for product cards -- GTIN, aggregateRating, category, return policy -- are almost always missing from default theme markup.

### GTIN/EAN/UPC -- High impact for price comparison

Perplexity uses GTINs to match products across retailers. Without a GTIN, Perplexity has to match your product by name and description, which is fuzzy and often fails. With a GTIN, Perplexity can confidently include your product in price comparisons -- which is where a lot of the shopping traffic comes from.

### Crawler access -- Table stakes

Your robots.txt must allow PerplexityBot. This sounds obvious, but we have seen Shopify stores that inadvertently block AI crawlers because of overly aggressive robots.txt rules or third-party security apps.

### Product data quality -- Medium impact, compounds over time

Perplexity's AI synthesizes product information from multiple sources. If your product page has specific, factual descriptions ("100% merino wool, 250gsm, crew neck, machine washable") rather than generic marketing copy ("The ultimate sweater you'll love"), Perplexity has better raw material to work with. This aligns with the broader principles of [AI Engine Optimization](/blog/what-is-aeo-shopify-guide/).

### IndexNow -- Indirect but real

PerplexityBot crawls the web independently, but Perplexity also uses Bing's index as a supplementary source. Sending IndexNow pings after product updates ensures Bing's index stays fresh, which benefits both your ChatGPT and Perplexity visibility.

**What to do:** Prioritize getting rich JSON-LD with GTINs on your product pages. This is the highest-leverage action for Perplexity specifically and AI search generally.

## What Doesn't Work or Is Unproven

We should be honest about what the data does NOT support:

- **llms.txt for Perplexity visibility.** As we covered in our [honest analysis of llms.txt](/blog/llms-txt-does-it-actually-work/), there is no documented evidence that PerplexityBot reads or uses llms.txt files. CDN logs across multiple sites show zero requests for `/llms.txt` from PerplexityBot. The file remains a speculative insurance policy, not a proven Perplexity optimization.
- **"Optimizing" product descriptions specifically for Perplexity.** Some consultants suggest writing product descriptions "in a way Perplexity prefers." There is no published Perplexity ranking algorithm, no preference documentation, and no evidence that Perplexity treats product descriptions differently from how any other search engine does. Write clear, specific, factual descriptions. That is the whole strategy.
- **Paying for Perplexity merchant placement.** As of early 2026, Perplexity does not offer a paid merchant program or advertising platform for product placement. If someone is charging you for "Perplexity optimization" as a service, ask them exactly what they are doing.
- **Social signals or backlinks as Perplexity ranking factors.** There is no evidence that Perplexity weights these signals the way traditional Google search does. Perplexity's ranking appears to be based primarily on relevance, source quality, and structured data completeness.

**What to do:** Be skeptical of any tactic that claims to be "Perplexity-specific optimization." The fundamentals -- structured data, GTINs, crawler access, data quality -- are universal across all AI search engines. There is no secret Perplexity hack.

## Perplexity vs. ChatGPT vs. Google AI Overviews: A Quick Comparison

| | **Perplexity** | **ChatGPT** | **Google AI Overviews** |
|---|---|---|---|
| **Primary index** | Own crawler + Bing/Google | Bing | Google |
| **Shopping UI** | Product cards, price comparison, Buy with Pro | Product cards via Shopify partnership | Product panels in search results |
| **GTIN usage** | Yes, for product matching | Yes, for product matching | Yes, for product matching |
| **Structured data** | Reads JSON-LD from crawled pages | Reads JSON-LD via Bing | Reads JSON-LD directly |
| **Source attribution** | Always cites sources with links | Sometimes cites, sometimes doesn't | Links to source pages |
| **Real-time data** | Always live web search | Live search when enabled | Live, integrated with Google Shopping |
| **Merchant volume** | Growing, smaller than ChatGPT/Google | Large (Shopify partnership) | Largest (Google Shopping integration) |

The practical takeaway: the optimization work is nearly identical across all three. Rich JSON-LD, GTINs, crawler access, and high-quality product data benefit you on every platform. The main difference is the indexing path: Perplexity crawls directly, ChatGPT goes through Bing, Google uses its own index.

## Action Pipeline for Shopify Merchants

Here is a concrete sequence. Do these in order:

**Immediate (today):**
1. Check `yourstore.com/robots.txt` for PerplexityBot blocks. Remove any `Disallow` for PerplexityBot, GPTBot, ChatGPT-User, ClaudeBot, and Google-Extended.
2. Search for your own products on perplexity.ai. Document what appears and what is missing.
3. Check your existing JSON-LD: view source on a product page, search for `application/ld+json`. Note what fields are present and what is missing.

**This week:**
4. Add GTINs (barcodes) to your Shopify product variants if they are missing. Products > Edit product > Variants > Barcode.
5. Enrich your JSON-LD to include category, color, material, brand, GTIN, aggregateRating, returnPolicy, and shippingDetails. Use a Theme App Extension if you don't want to edit theme code.
6. Set up IndexNow notifications so Bing gets pinged when you update products.

**Ongoing:**
7. Monitor your product appearances on Perplexity, ChatGPT, and Google AI Overviews monthly.
8. When adding new products, ensure structured data is complete before publishing.
9. Keep product descriptions specific and factual. Every product should have enough detail that an AI could recommend it without needing to infer anything.

## Getting Started

If you want to automate most of this pipeline, [Agentic Flow](https://apps.shopify.com/agentic-flow-aeo-metafields) handles the heavy lifting: it uses Google Gemini to analyze your product images and extract structured attributes (category, color, material), injects rich Schema.org JSON-LD via a Theme App Extension, sends IndexNow pings after every scan, generates a spec-compliant llms.txt, and gives you an AEO Score dashboard to track your progress. Free for up to 20 products.

But regardless of what tool you use, the fundamentals don't change. Perplexity, ChatGPT, and Google AI Overviews all run on the same basic fuel: structured, accurate, complete product data. The merchants who treat their product data as infrastructure -- not an afterthought -- are the ones who will show up when AI-powered shoppers come looking.

---

*Learn more: [What is AEO? The complete Shopify guide](/blog/what-is-aeo-shopify-guide/) | [How to appear in ChatGPT recommendations](/blog/shopify-products-chatgpt-recommendations/) | [The honest truth about llms.txt](/blog/llms-txt-does-it-actually-work/)*
