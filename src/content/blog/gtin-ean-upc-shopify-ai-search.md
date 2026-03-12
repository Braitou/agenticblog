---
title: 'GTIN, EAN, UPC: Why Product Identifiers Became Mandatory for AI Search'
description: 'AI shopping platforms use GTINs to match and recommend products. Most Shopify stores leave the barcode field empty. Here is why that is costing you visibility in ChatGPT, Perplexity, and Google Shopping.'
pubDate: 2026-03-12
---

There's a field in your Shopify product editor that most merchants ignore. It's labeled "Barcode (ISBN, UPC, GTIN, etc.)" and it sits right below the SKU input on every variant.

That field might be the single biggest reason your products don't appear in AI shopping results.

We've analyzed structured data across hundreds of Shopify stores. The pattern is consistent: stores with GTINs in their product data show up in ChatGPT Shopping and Perplexity Shopping at significantly higher rates than stores without them. Not because of some secret algorithm hack — but because of how product matching fundamentally works in AI systems.

## What Are GTINs, EANs, and UPCs?

Let's cut through the acronym soup.

All three are **Global Trade Item Numbers** — unique numeric codes assigned to a specific product. They're the barcode on the physical packaging. The differences are mostly regional and historical:

- **UPC** (Universal Product Code): 12 digits. Standard in North America. The barcode you see on everything at Walmart or Target.
- **EAN** (European Article Number): 13 digits. Standard in Europe and most of the world. Also called GTIN-13.
- **GTIN** (Global Trade Item Number): The umbrella term. GTIN-12 is a UPC, GTIN-13 is an EAN, GTIN-14 is for cases/pallets.

In practice, when someone says "GTIN," they mean the barcode number on your product. Whether it's 12 or 13 digits, it serves the same purpose: **uniquely identifying a specific product across every retailer and platform on the planet.**

A Nike Air Force 1 '07 in white, size 10, has the same GTIN whether it's sold on Nike.com, Amazon, Foot Locker, or your Shopify store. That's the entire point.

## Why AI Shopping Platforms Need GTINs

Here's the core problem AI shopping engines face: **matching products across the internet.**

When someone asks ChatGPT "What's the best price for a Sony WH-1000XM5?", the system needs to find that exact product across hundreds of retailers and compare them. Product names are unreliable — one store calls it "Sony WH-1000XM5 Wireless Noise Cancelling Headphones," another calls it "Sony WH1000XM5/B Over-Ear Bluetooth ANC Headset." Same product, totally different titles.

GTINs solve this instantly. The barcode number `4548736132191` maps to exactly one product in the world: the Sony WH-1000XM5 in black. No ambiguity. No fuzzy matching. No guesswork.

This is why every major AI shopping platform relies on them:

- **ChatGPT Shopping** uses Bing's product database and Shopify's merchant feed. Both use GTINs as the primary product identifier for matching and deduplication.
- **Google Shopping** (and Google AI Overviews) has required GTINs for years. Products without them get lower visibility and can't participate in price comparisons.
- **Perplexity Shopping** crawls the web and reads structured data. When your JSON-LD includes a GTIN, Perplexity can confidently identify your product and include it in comparison results.
- **Microsoft Copilot Shopping** uses Bing's product graph — same GTIN dependency as ChatGPT.

Without a GTIN, these platforms have to rely on fuzzy name matching. That works sometimes. It fails often. And when it fails, your product simply doesn't appear.

## The Shopify Problem: Empty Barcode Fields

Here's what we see across the Shopify ecosystem:

**Most stores leave the barcode field empty.** Especially DTC (direct-to-consumer) brands, dropshippers, and stores selling handmade or private-label products. The field feels optional because Shopify doesn't require it. Your store works fine without it. Customers can still buy your products.

But "works fine for humans" and "works fine for AI" are two different things.

When the barcode field is empty, three things happen:

1. **Your JSON-LD has no GTIN.** Most themes and apps pull the barcode from Shopify's product data to populate the `gtin13` or `gtin12` field in Schema.org markup. No barcode in Shopify = no GTIN in structured data = invisible to AI product matching.
2. **Google Merchant Center flags your products.** Google has been increasingly penalizing products without GTINs in Shopping feeds. Lower visibility, fewer impressions, no price comparison eligibility.
3. **ChatGPT Shopping can't match you.** When a user asks for product comparisons or "best price for X," ChatGPT needs GTINs to build those comparison tables. Without one, you're excluded.

## "But My Products Don't Have Barcodes"

This is the most common pushback. Let's address the different scenarios:

### You resell branded products

**You almost certainly have GTINs.** The manufacturer assigned them. Check the physical packaging — the barcode number is your GTIN. You can also search the brand's product catalog, or use databases like [Open Food Facts](https://openfoodfacts.org) or [Barcode Lookup](https://www.barcodelookup.com) to find them.

**What to do:** Enter the barcode number in Shopify's barcode field for each variant. Yes, each *variant* — different sizes, colors, and configurations have different GTINs.

### You sell private-label or white-label products

**You need to get GTINs.** The official source is [GS1](https://www.gs1.org/), the global organization that manages the GTIN system. In the US, that's [GS1 US](https://www.gs1us.org/). You purchase a company prefix, which gives you a range of GTINs you can assign to your products.

Cost: GS1 US charges a one-time fee starting around $250 for 10 GTINs, plus an annual renewal fee of $50. For most brands, this is a no-brainer investment given the visibility it unlocks.

**What to do:** Register with your local GS1 office, get your prefix, assign GTINs to each product/variant, and enter them in Shopify.

### You sell handmade or truly unique products

**You may not need GTINs — but you need something.** If each product is genuinely one-of-a-kind (art, custom jewelry, vintage items), GTINs don't apply. In this case, use the `mpn` (Manufacturer Part Number) field in your structured data with your own internal identifier, and make sure your JSON-LD is rich in other attributes: material, category, color, dimensions.

Google's documentation explicitly exempts handmade and vintage products from the GTIN requirement, and AI shopping platforms follow the same logic.

### You dropship

**The GTINs exist — you just need to find them.** Your supplier has them. Ask for a product feed that includes barcodes. If they can't provide one, that's a red flag about the supplier, not a GTIN problem.

## How GTINs Should Appear in Your Structured Data

Having the barcode in Shopify is step one. Step two is making sure it appears correctly in your Schema.org JSON-LD markup. Here's what AI engines expect to see:

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Sony WH-1000XM5 Wireless Noise Cancelling Headphones",
  "brand": {
    "@type": "Brand",
    "name": "Sony"
  },
  "gtin13": "4548736132191",
  "sku": "WH1000XM5-B",
  "offers": {
    "@type": "Offer",
    "price": "348.00",
    "priceCurrency": "USD",
    "availability": "https://schema.org/InStock"
  }
}
```

Key points:

- **Use the right field name.** 12-digit barcode → `gtin12`. 13-digit barcode → `gtin13`. 14-digit → `gtin14`. Or just use the generic `gtin` field, which accepts any length.
- **It's a string, not a number.** GTINs can have leading zeros. `"0012345678905"` is valid. `12345678905` drops the leading zero and becomes invalid.
- **One GTIN per variant.** If your product has 5 color variants, each should have its own GTIN in the structured data for that specific variant page or variant selection.
- **Don't confuse GTIN with SKU.** Your SKU is your internal identifier. The GTIN is the universal one. Both should be in your JSON-LD, but they serve different purposes.

## How to Check If Your Store Has GTINs Set Up Correctly

Here's a quick audit:

1. **Check Shopify Admin.** Go to Products → select a product → scroll to the variant section. Is the "Barcode" field filled in? Do this for your top 20 products.
2. **Check your storefront.** Visit a product page, right-click → View Page Source, and search for `gtin`. If you don't find it, your JSON-LD isn't including the barcode even if it exists in Shopify.
3. **Use Google's Rich Results Test.** Paste a product URL into [Google's Rich Results Test](https://search.google.com/test/rich-results). Look for the Product result — does it show a GTIN field?
4. **Check Google Merchant Center.** If you're connected, look at the Diagnostics tab. Google explicitly flags products with missing GTINs.

If step 1 passes but step 2 fails, your theme or JSON-LD app isn't pulling the barcode field. That's a configuration issue, not a data issue.

## The Compound Effect: GTIN + JSON-LD + IndexNow

GTINs don't work in isolation. They're one piece of the AI visibility pipeline:

1. **GTIN in Shopify** → your product has a universal identifier
2. **GTIN in JSON-LD** → search engines and AI crawlers can read it
3. **IndexNow ping** → Bing re-crawls your page and picks up the GTIN
4. **ChatGPT/Perplexity/Copilot** → can now match your product in shopping queries

Skip any step and the chain breaks. A GTIN in Shopify that doesn't appear in your JSON-LD is useless for AI. A GTIN in JSON-LD that Bing hasn't crawled yet is invisible. The full pipeline matters.

## What We're Seeing in Practice

We won't make claims we can't back up. Here's what we observe:

- Products with GTINs in their JSON-LD appear in **Google Rich Results** at higher rates than products without them. Google has documented this publicly.
- ChatGPT Shopping comparison tables almost exclusively feature products that have GTINs. Try asking ChatGPT to compare prices on any branded product — the results map to GTIN-identified products.
- Stores that add GTINs and then trigger an IndexNow re-crawl see their products appear in **Bing Shopping** (which feeds ChatGPT) within days, not weeks.
- Google Merchant Center's diagnostic data consistently shows that GTIN-missing products get fewer impressions and clicks in Shopping results.

This isn't a theoretical advantage. It's the documented behavior of every major shopping platform, now amplified by AI.

## Getting Started

If you have 50 products, you can manually add barcodes in Shopify Admin in an afternoon. For larger catalogs, use Shopify's CSV import/export to bulk-update the barcode field.

Once your barcodes are in Shopify, you need them reflected in your storefront's structured data. [Agentic Flow](https://apps.shopify.com/agentic-flow-aeo-metafields) automatically pulls your Shopify barcodes into rich Schema.org JSON-LD markup — along with category, color, material, brand, and all the other attributes AI engines look for. It also sends IndexNow notifications so Bing picks up the changes fast. Free for up to 20 products.

But whatever tool you use, the priority is clear: **fill in your barcode fields, make sure they appear in your structured data, and notify search engines.** GTINs are no longer a nice-to-have. For AI shopping, they're the primary key.

---

*Want the full picture? Read our [guide to getting your products into ChatGPT](/blog/shopify-products-chatgpt-recommendations/) or learn how to [set up IndexNow on your Shopify store](/blog/indexnow-shopify-guide/).*
