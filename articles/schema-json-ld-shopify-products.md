---
title: 'Schema.org JSON-LD for Shopify Products: What AI Engines Actually Want to See'
description: 'Most Shopify stores have broken or incomplete JSON-LD. Here is exactly what fields matter for AI search engines and how to fix yours.'
pubDate: 2026-03-03
---

Your Shopify store probably already has JSON-LD on its product pages. Every modern Shopify theme injects some form of it. And that is exactly the problem -- most merchants assume this means they are covered, when in reality their structured data is so thin that AI engines treat it as noise.

We audited dozens of Shopify stores across different themes and price points. The pattern is consistent: the default JSON-LD includes a product name, a price, an image URL, and maybe an availability status. That is roughly 20% of what AI search engines can actually use. The other 80% -- the fields that help ChatGPT, Perplexity, and Google AI Overviews decide which products to recommend -- is missing entirely.

In our [complete AEO guide](/blog/what-is-aeo-shopify-guide/), we called structured data the number one pillar of AI Engine Optimization. This article is the deep dive: exactly what fields matter, what Shopify gets wrong by default, and how to fix it.

## What Is JSON-LD and Why AI Engines Depend on It

JSON-LD (JavaScript Object Notation for Linked Data) is a structured data format that sits inside a `<script>` tag in your page's HTML. It uses the Schema.org vocabulary to describe your product in a way that any machine can parse instantly -- no scraping, no guessing, no natural language processing needed.

Here is why this matters for AI search specifically:

**ChatGPT Search** uses Bing's index as its primary backend. When Bing crawls your product page, it reads your JSON-LD to build its understanding of what you sell: product name, price, availability, brand, identifiers, reviews. That structured understanding is what ChatGPT draws from when a user asks "What is the best leather messenger bag under $200?"

**Perplexity** similarly relies on search indexes that consume structured data. When it builds its shopping answers, it pulls product attributes directly from JSON-LD markup.

**Google AI Overviews** are powered by Google's Knowledge Graph, which has been consuming Schema.org structured data for over a decade.

The pattern across all of these: AI engines do not read your marketing copy and decide to recommend you. They read your structured data, compare it against other products, and surface the ones with the most complete and accurate machine-readable information.

**What to do:** Accept that JSON-LD is not a technical checkbox. It is the primary interface between your products and AI search engines. Treat it accordingly.

## What Shopify Generates by Default

Most Shopify themes -- Dawn, Refresh, and the majority of third-party themes -- inject a basic `Product` schema via their theme Liquid templates. Typically you get something like this:

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Leather Messenger Bag",
  "image": "https://cdn.shopify.com/s/.../bag.jpg",
  "offers": {
    "@type": "Offer",
    "price": "129.00",
    "priceCurrency": "USD",
    "availability": "https://schema.org/InStock"
  }
}
```

That is it. Four fields inside a bare-bones Offer object. No brand. No category. No color or material. No GTIN. No reviews. No return policy. No shipping details.

From Google's perspective, this might get you a basic price snippet in search results. From an AI engine's perspective, this product is a ghost -- it exists, but there is nothing meaningful to compare it against when a user asks a specific product question.

**What to do:** View source on one of your product pages right now. Search for `application/ld+json` and look at what is actually there. If it looks like the example above, everything that follows in this article applies to you.

## The Critical Fields Most Stores Miss

Here are the fields that separate stores AI engines recommend from stores they ignore, in order of impact:

### GTIN / EAN / UPC

This is the big one. Global Trade Item Numbers are how AI shopping platforms identify your product across the entire internet. ChatGPT Shopping and Perplexity Shopping use GTINs to match products, verify pricing, and build trusted product profiles. Without a GTIN, AI shopping platforms fall back to fuzzy name matching -- which fails more often than it works. We covered this in detail in our [ChatGPT recommendations guide](/blog/shopify-products-chatgpt-recommendations/).

### brand

Most Shopify themes do not output a `brand` property at all. AI engines use brand as a primary filter in product comparisons. When a user asks "best Nike running shoes under $150," ChatGPT needs to know which products belong to Nike -- and it reads that from your JSON-LD `brand` field, not from your product title.

### aggregateRating

If you have product reviews, they should appear in your JSON-LD as an `aggregateRating` object with `ratingValue` and `reviewCount`. AI engines use review data as a quality signal when deciding which products to recommend. A product with a 4.7-star rating across 230 reviews is far more likely to be surfaced than one with no rating data at all.

### category / additionalProperty

Specific product categorization helps AI engines match your products to user queries. "Leather Messenger Bag" is vastly more useful than "Accessories." Structured properties like color and material, expressed via `additionalProperty` or their dedicated Schema.org fields (`color`, `material`), let AI engines filter and compare at a granular level.

### offers (complete)

The minimal Offer object is not enough. A complete offers block should include `priceValidUntil` (tells engines the price is current), `itemCondition`, `seller`, and `url` pointing to the specific product page. For shipping and returns, `shippingDetails` and `hasMerchantReturnPolicy` are what qualify you for Google's enhanced rich results -- and they give AI engines the data they need to answer questions like "Does this store offer free shipping?"

**What to do:** Check your JSON-LD for each of these fields. Every one that is missing is a missed signal to AI engines.

## Minimal vs. Complete JSON-LD: Side by Side

Here is what most Shopify stores have versus what AI engines actually want to see.

**What most stores have:**

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Leather Messenger Bag",
  "image": "https://cdn.shopify.com/s/.../bag.jpg",
  "offers": {
    "@type": "Offer",
    "price": "129.00",
    "priceCurrency": "USD",
    "availability": "https://schema.org/InStock"
  }
}
```

**What a complete, AI-optimized JSON-LD block looks like:**

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Leather Messenger Bag",
  "url": "https://yourstore.com/products/leather-messenger-bag",
  "image": [
    "https://cdn.shopify.com/s/.../bag-front.jpg",
    "https://cdn.shopify.com/s/.../bag-side.jpg"
  ],
  "description": "Full-grain vegetable-tanned leather messenger bag with adjustable shoulder strap, brass hardware, and padded 15-inch laptop compartment.",
  "brand": {
    "@type": "Brand",
    "name": "YourBrand"
  },
  "category": "Messenger Bags",
  "color": "Brown",
  "material": "Full-grain leather",
  "gtin13": "5901234123457",
  "sku": "MSG-BRN-001",
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.7",
    "reviewCount": "142"
  },
  "offers": {
    "@type": "Offer",
    "url": "https://yourstore.com/products/leather-messenger-bag",
    "price": "129.00",
    "priceCurrency": "USD",
    "availability": "https://schema.org/InStock",
    "itemCondition": "https://schema.org/NewCondition",
    "priceValidUntil": "2026-12-31",
    "shippingDetails": {
      "@type": "OfferShippingDetails",
      "shippingRate": {
        "@type": "MonetaryAmount",
        "value": "0",
        "currency": "USD"
      },
      "deliveryTime": {
        "@type": "ShippingDeliveryTime",
        "handlingTime": {
          "@type": "QuantitativeValue",
          "minValue": 0,
          "maxValue": 1,
          "unitCode": "DAY"
        },
        "transitTime": {
          "@type": "QuantitativeValue",
          "minValue": 3,
          "maxValue": 7,
          "unitCode": "DAY"
        }
      }
    },
    "hasMerchantReturnPolicy": {
      "@type": "MerchantReturnPolicy",
      "returnPolicyCategory": "https://schema.org/MerchantReturnFiniteReturnWindow",
      "merchantReturnDays": 30,
      "returnMethod": "https://schema.org/ReturnByMail",
      "returnFees": "https://schema.org/FreeReturn"
    }
  }
}
```

Count the difference. The first block has 5 meaningful properties. The second has over 25 -- including brand, GTIN, reviews, shipping, returns, color, material, and a proper description. When an AI engine compares products, which one do you think gets recommended?

**What to do:** Use the complete example above as your target. You do not need every single field on day one, but prioritize brand, GTIN, aggregateRating, and complete offers data.

## How to Test Your JSON-LD

Three tools, in order of usefulness:

**1. Google Rich Results Test** (search.google.com/test/rich-results) -- Paste a product URL and Google will show you exactly which structured data it detects, which fields are present, and which are missing or have errors. This is the gold standard.

**2. Schema Markup Validator** (validator.schema.org) -- Tests your markup against the full Schema.org specification. More permissive than Google's tool, but useful for catching syntax errors and structural problems.

**3. View source** -- The most underrated test. Go to your product page, right-click, "View Page Source," and search for `application/ld+json`. Read the raw JSON. Is it what you expect? Does it have the fields you think it has? We have seen cases where a Shopify app claims to inject JSON-LD but the block is empty or malformed in production.

**What to do:** Run your top 5 product URLs through Google's Rich Results Test this week. Write down every warning and missing field. That is your fix list.

## Common Mistakes That Break Your JSON-LD

After looking at hundreds of Shopify stores, these are the mistakes we see most often:

### Duplicate schemas

This is the most common issue. Your theme outputs a basic Product JSON-LD block. Then a Shopify app injects a second, richer one. Now the page has two competing Product schemas, and search engines have to guess which one is authoritative. Some will merge them. Some will pick one at random. Some will throw warnings and potentially ignore both.

**Fix:** Check view-source for multiple `application/ld+json` script tags with `"@type": "Product"`. If you find duplicates, disable the theme's built-in JSON-LD before adding your own. Most Theme App Extensions handle this automatically by suppressing the theme's default output.

### Wrong price format

Schema.org expects price as a string without currency symbols or thousands separators. `"price": "1,299.00"` is invalid (the comma breaks parsing). `"price": "$129.00"` is invalid (the dollar sign). The correct format is `"price": "129.00"`.

**Fix:** Validate that your price values are clean decimal numbers without symbols or commas.

### Missing or incorrect availability URLs

The `availability` field must be a full Schema.org URL, not a plain text value. `"availability": "InStock"` is wrong. `"availability": "https://schema.org/InStock"` is correct. The valid values are `InStock`, `OutOfStock`, `PreOrder`, `BackOrder`, `SoldOut`, and `Discontinued` -- all as full `https://schema.org/` URLs.

### Stale data

Your JSON-LD says the product is in stock, but it is actually sold out. Or the price in the JSON-LD does not match the price displayed on the page. Google explicitly penalizes mismatches between structured data and visible page content, and AI engines inherit this penalty through search indexes.

**Fix:** Make sure your JSON-LD is dynamically rendered from your product's current data, not hardcoded or cached from a previous scan.

**What to do:** Run through these four mistakes on your store. They account for the vast majority of JSON-LD issues we encounter.

## The Action Pipeline

Here is a concrete, ordered plan you can execute this week:

1. **Audit (15 minutes).** View source on 3-5 product pages. Search for `application/ld+json`. Document what fields are present and what is missing.

2. **Test (15 minutes).** Run those same URLs through Google's Rich Results Test. Note every warning and error.

3. **Check for duplicates (10 minutes).** Count how many Product JSON-LD blocks exist on each page. If more than one, you need to resolve that first.

4. **Add barcodes (30 minutes).** Go to Shopify Admin > Products and add barcodes (GTIN/EAN/UPC) to your top products. These are the product identifiers that AI shopping platforms use to match and verify products.

5. **Enrich your JSON-LD (varies).** Either manually edit your theme's Liquid templates to add the missing fields, or install a Theme App Extension that handles this. The complete example earlier in this article is your target.

6. **Validate again (15 minutes).** Re-run the Rich Results Test after making changes. Confirm the new fields are appearing correctly.

7. **Notify search engines.** Send IndexNow pings for every product page you updated. This gets Bing (and by extension ChatGPT) to re-crawl your updated structured data within hours instead of weeks.

## The Bigger Picture

JSON-LD is the foundation, but it is not the whole building. As we covered in our [llms.txt analysis](/blog/llms-txt-does-it-actually-work/), a complete AEO strategy combines structured data with product data quality, search engine notification (IndexNow), and proper crawler access. No single piece is sufficient on its own.

But if you had to pick one thing to fix first -- one lever that has the most documented, reproducible impact on AI visibility -- it is your JSON-LD. Fix that, and everything else builds on top of a solid base.

If you want to automate this pipeline, [Agentic Flow](https://apps.shopify.com/agentic-flow-aeo-metafields) scans your product images with Google Gemini to extract structured attributes (category, color, material), then injects complete Schema.org JSON-LD via a Theme App Extension, sends IndexNow pings, generates llms.txt, and tracks everything through an AEO Score dashboard. Free for up to 20 products.

But regardless of what tool you use, the fields and principles in this article are what matter. AI engines want structured, complete, accurate product data in a format they can parse instantly. JSON-LD is that format. Make yours count.

---

*Read more: [The complete AEO guide for Shopify merchants](/blog/what-is-aeo-shopify-guide/) | [How to get your products into ChatGPT](/blog/shopify-products-chatgpt-recommendations/) | [The honest truth about llms.txt](/blog/llms-txt-does-it-actually-work/)*
