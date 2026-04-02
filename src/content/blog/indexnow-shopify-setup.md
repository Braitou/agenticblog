---
title: 'IndexNow for Shopify: How to Get Your Products Indexed by Bing and ChatGPT in Minutes'
description: 'IndexNow is the fastest way to get your Shopify product pages into Bing''s index and ChatGPT Search. Here is how the pipeline works and three ways to set it up on your store.'
pubDate: 2026-04-02
---

You update a product title, tweak a description, adjust pricing. Then you wait. Days. Sometimes weeks. Hoping Bing's crawler notices your changes and updates its index.

Meanwhile, a shopper asks ChatGPT "What's the best organic dog food for sensitive stomachs?" and your freshly updated product page -- the one with the perfect answer to that question -- sits invisible because Bing hasn't re-crawled it yet.

This is the indexing gap. And IndexNow closes it.

IndexNow is an open protocol that lets you ping search engines the moment a URL changes. Instead of waiting for crawlers to discover your updates on their own schedule, you tell them directly: "This page changed. Come get it." Bing typically processes these notifications within minutes to hours.

For Shopify merchants trying to get products into ChatGPT Search, Perplexity, and Microsoft Copilot, IndexNow is the most proven, most documented mechanism available. Here is exactly how it works and three ways to set it up on your store.

## What Is IndexNow and Why Shopify Merchants Need It

IndexNow is a protocol created by Microsoft (Bing) and Yandex in 2021. It provides a simple API that website owners use to notify search engines about URL changes -- new pages, updated pages, or deleted pages. Instead of relying on crawlers to find changes passively, you push the information to them.

The adoption numbers tell the story. Over 80 million websites now use IndexNow, submitting more than 5 billion URLs per day. The protocol is supported by Bing, Yandex, Naver, Seznam.cz, and Yep. Major platforms like LinkedIn, eBay, GitHub, and Wix have adopted it natively.

For Shopify merchants specifically, IndexNow solves a critical timing problem. Traditional crawling means your product updates can take days or weeks to appear in search indexes. With IndexNow, the path from product update to search index entry shrinks to minutes or hours.

Why does this matter for e-commerce?

- **Price changes need to be reflected immediately.** If you drop a price by 30%, you want that showing up in AI shopping results today, not next week.
- **New product launches are time-sensitive.** A seasonal collection that takes two weeks to get indexed misses the buying window.
- **Inventory updates affect the customer experience.** If a product goes out of stock but Bing still shows it as available, that creates a bad experience for the shopper and the AI that recommended it.
- **Product data enrichment should be visible fast.** When you [improve your structured data](/blog/what-is-aeo-shopify-guide/) -- adding GTINs, reviews, rich schema -- you want AI engines to pick up those improvements quickly.

## The IndexNow-to-ChatGPT Pipeline (How It Works)

This is the part most articles skip. Let's look at the actual plumbing.

### IndexNow to Bing to ChatGPT Search (The Proven Chain)

ChatGPT Search uses Bing's index as its primary data source for web results. This is well-documented -- OpenAI and Microsoft have a multi-billion dollar partnership, and Bing's crawl data powers the search results you see when ChatGPT browses the web.

The chain works like this:

1. **You send an IndexNow ping** with your updated product URL
2. **Bing receives the notification** and prioritizes crawling that URL
3. **Bing re-crawls your page** and reads the updated content, structured data, and schema markup
4. **Bing updates its index** with the new information
5. **ChatGPT Search queries Bing's index** when a user asks a product-related question
6. **Your updated product data appears** in ChatGPT's response

Steps 1 through 4 typically happen within minutes to hours. Step 5 happens whenever a relevant query occurs.

This is not theoretical. It is the most reproducible AI search optimization mechanism available. Bing's own Webmaster Tools now includes an "AI Performance" dashboard that shows publishers how often their content gets cited in Microsoft Copilot and Bing's AI-generated answers. IndexNow submissions directly feed this pipeline.

Microsoft Copilot and Perplexity also benefit from this chain because they use Bing's index as a data source. When you ping IndexNow, you are effectively updating your product information across multiple AI search surfaces simultaneously.

One important caveat: Google does not support IndexNow. Despite testing the protocol since 2021, Google continues to rely on its own crawling infrastructure. We will cover the Google side separately in the comparison section below.

## How to Set Up IndexNow on Shopify (3 Methods)

Shopify does not natively support IndexNow out of the box. You need to add it yourself. Here are three approaches, ordered from simplest to most powerful.

### Method 1: Manual API Setup (Free)

This is the bare-bones approach. It costs nothing and gives you full control, but requires you to manually submit URLs each time you make changes.

**Step 1: Generate an API key**

Your IndexNow API key is a string of 8 to 128 hexadecimal characters. You can generate one with any UUID generator -- just remove the dashes if you want a clean key. Example:

```
a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6
```

**Step 2: Host the key verification file**

IndexNow needs to verify you own the domain. Create a text file named `{your-key}.txt` containing just the key itself. For the example above, the file would be named `a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6.txt` and contain the text `a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6`.

On Shopify, hosting a file at your domain root is not straightforward. The simplest approach: upload the key file to Shopify's Files section (Settings > Files), then create a URL redirect from `/{your-key}.txt` to the uploaded file's CDN URL. Alternatively, if your theme supports it, you can add the file through the theme's Assets folder.

**Step 3: Submit URLs via GET request**

For a single URL, you can submit via a simple GET request in your browser:

```
https://api.indexnow.org/indexnow?url=https://your-store.com/products/your-product&key=a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6
```

A `200 OK` or `202 Accepted` response means it worked.

**Step 4: Batch submit via POST (for multiple URLs)**

For multiple URLs at once, send a POST request to `https://api.indexnow.org/indexnow` with this JSON body:

```json
{
  "host": "your-store.com",
  "key": "a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6",
  "urlList": [
    "https://your-store.com/products/product-one",
    "https://your-store.com/products/product-two",
    "https://your-store.com/products/product-three"
  ]
}
```

You can submit up to 10,000 URLs per request. Use `Content-Type: application/json; charset=utf-8`.

**Pros:** Free, no third-party dependencies, you control everything.

**Cons:** Entirely manual. You need to remember to submit URLs after every product change. For a store with 50+ products that change regularly, this becomes unsustainable fast.

### Method 2: Using a Shopify App

This is the most practical option for most merchants. Several Shopify apps handle IndexNow submissions automatically whenever your products change.

What to look for in an IndexNow app:

- **Automatic detection of product changes** -- the app should fire IndexNow pings whenever you create, update, or delete a product without you doing anything
- **Batch submission support** -- the app should submit multiple URLs efficiently, not one at a time
- **Key hosting handled for you** -- no manual file uploads or redirects
- **Submission logs** -- you should be able to see which URLs were submitted and the response codes

[Agentic Flow](https://apps.shopify.com/agentic-flow-aeo-metafields) handles IndexNow as part of its broader AEO pipeline -- it automatically pings IndexNow after scanning your products and updating their structured data. This means your product pages get re-indexed with the enriched JSON-LD, [GTINs](/blog/gtin-ean-upc-shopify-ai-search/), and schema markup already in place, which is the ideal sequence: improve the data first, then tell Bing to come read it.

Other apps like TinyIMG and InstaIndex also offer IndexNow functionality as standalone features. Pick whatever fits your workflow.

**Pros:** Fully automated, no technical knowledge required, set-and-forget.

**Cons:** Monthly app cost, dependent on the app continuing to function correctly.

### Method 3: Custom Webhook Integration (For Developers)

If you have development resources and want full control with full automation, you can build a custom integration using Shopify webhooks and a lightweight server.

The architecture:

1. **Shopify fires a webhook** when a product is created or updated (`products/create`, `products/update`)
2. **Your server receives the webhook** payload containing the product data
3. **Your server constructs the product URL** from the payload (e.g., `https://your-store.com/products/{handle}`)
4. **Your server sends an IndexNow API call** with the product URL

Here is a minimal Node.js example for the server-side handler:

```javascript
const express = require('express');
const app = express();
app.use(express.json());

const INDEXNOW_KEY = 'your-api-key-here';
const STORE_DOMAIN = 'your-store.com';

app.post('/webhooks/product-update', async (req, res) => {
  const product = req.body;
  const productUrl = `https://${STORE_DOMAIN}/products/${product.handle}`;

  try {
    const response = await fetch('https://api.indexnow.org/indexnow', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json; charset=utf-8' },
      body: JSON.stringify({
        host: STORE_DOMAIN,
        key: INDEXNOW_KEY,
        urlList: [productUrl]
      })
    });

    console.log(`IndexNow response: ${response.status} for ${productUrl}`);
    res.status(200).send('OK');
  } catch (error) {
    console.error('IndexNow submission failed:', error);
    res.status(500).send('Error');
  }
});

app.listen(3000);
```

To register the webhook in Shopify, go to **Settings > Notifications > Webhooks** and add a webhook for the `Product update` event, pointing to your server's endpoint URL.

You can extend this to handle collection updates, blog posts, page changes, and bulk operations. For stores with large catalogs, add a queue (like Redis or SQS) to batch URLs and submit them in groups of up to 10,000.

**Pros:** Full control, no app costs, works exactly the way you need it to, can integrate with your existing infrastructure.

**Cons:** Requires development resources, server hosting costs, you are responsible for uptime and maintenance.

## Verifying IndexNow Is Working

Setting it up is one thing. Knowing it is actually working is another. Here is how to verify.

**Check the API response codes.** When you submit a URL to IndexNow, the response tells you what happened:

| Code | Meaning |
|------|---------|
| 200 OK | URL successfully submitted |
| 202 Accepted | Received, will be processed |
| 400 Bad Request | Invalid format -- check your JSON |
| 403 Forbidden | Key verification failed -- check your key file |
| 422 Unprocessable | URL doesn't match the host or key |
| 429 Too Many Requests | You are being rate-limited |

**Use Bing Webmaster Tools.** This is the definitive verification. Sign up at [Bing Webmaster Tools](https://www.bing.com/webmasters/), verify your Shopify domain, and check the IndexNow section. It shows you exactly which URLs were submitted, when they were processed, and whether they resulted in a crawl.

**Check the "AI Performance" dashboard.** Bing recently launched an AI Performance report in Webmaster Tools that shows how often your pages are cited in Microsoft Copilot and Bing AI answers. If your IndexNow submissions are working, you should see your freshly updated product pages appearing in this report.

**Inspect Bing's cached version.** Search for your product URL on Bing and check the cached date. If IndexNow is working, the cached version should reflect your most recent changes within hours, not weeks.

**Monitor your structured data.** IndexNow only tells Bing to re-crawl your page. What Bing finds when it arrives is what matters. Use Google's Rich Results Test or Schema.org's validator to make sure your JSON-LD is complete and correct before submitting. There is no point rushing Bing to a page with broken structured data.

## IndexNow vs. Google Indexing API

Merchants often ask: "Should I use IndexNow or the Google Indexing API?" The answer is both, but for different reasons and with different expectations.

| | IndexNow | Google Indexing API |
|---|---|---|
| **Supported engines** | Bing, Yandex, Naver, Seznam, Yep | Google only |
| **AI search impact** | Direct (ChatGPT, Copilot, Perplexity via Bing) | Indirect (Google AI Overviews) |
| **Content restrictions** | None -- any URL type | Officially limited to JobPosting and BroadcastEvent schema |
| **Setup complexity** | Simple API key + verification file | OAuth 2.0, Google Cloud service account, complex auth flow |
| **Daily URL limit** | 10,000 per request, no hard daily cap | 200 URLs per day default quota |
| **Batch submission** | Up to 10,000 URLs per POST | Individual URL submissions |
| **Cost** | Free | Free (but Google Cloud project required) |

The practical reality: the Google Indexing API is officially restricted to job postings and livestream content. Many SEOs use it for other content types and it sometimes works, but Google does not guarantee it will process non-qualifying URLs. There are also reports of sites getting their quota reduced or submissions ignored when used outside the intended scope.

IndexNow, by contrast, has no content type restrictions. Product pages, collection pages, blog posts -- everything is fair game.

For Shopify merchants focused on [AI search visibility](/blog/shopify-products-chatgpt-recommendations/), IndexNow provides the most direct and reliable path. ChatGPT Search uses Bing. Copilot uses Bing. Perplexity uses Bing. The pipeline is clear and proven. Google AI Overviews uses Google's own index, which IndexNow does not feed into, but traditional sitemaps and Google Search Console handle that side.

The best strategy: use IndexNow for the Bing/AI pipeline and maintain a well-structured sitemap for Google. They are complementary, not competing.

## FAQ

**Does IndexNow guarantee my products will appear in ChatGPT?**

No. IndexNow guarantees that Bing will re-crawl your page quickly. Whether ChatGPT then recommends your product depends on data quality, relevance to the query, [structured data completeness](/blog/what-is-aeo-shopify-guide/), pricing competitiveness, and many other factors. IndexNow removes the indexing delay -- it does not replace the need for good product data.

**How often should I submit URLs?**

Only when something changes. IndexNow is designed for change notifications, not periodic pings. Submitting unchanged URLs repeatedly will not help and may trigger rate limiting (429 responses). If you update a product, submit it. If nothing changed, don't.

**Does IndexNow help with Google rankings?**

Not directly. Google does not support IndexNow. However, having fresh, well-structured content indexed quickly on Bing can indirectly benefit your overall search presence if your content gets cited across AI platforms and generates backlinks or brand mentions.

**Can I use IndexNow for collection pages and blog posts, not just products?**

Yes. IndexNow works for any URL on your domain. Product pages, collection pages, blog posts, your homepage -- anything that changes and needs re-indexing.

**What happens if my key verification file is not accessible?**

IndexNow will return a 403 Forbidden error and reject your submission. The verification file must be accessible at `https://your-domain.com/{your-key}.txt` and contain the key. Double-check that Shopify is not blocking or redirecting the file path.

**Is there a cost to using IndexNow?**

The protocol itself is free. The only costs come from how you implement it -- whether that is an app subscription, server hosting for a custom integration, or your own time for manual submissions.

**I already have a sitemap. Why do I need IndexNow?**

Sitemaps tell search engines what pages exist on your site. Crawlers check sitemaps periodically -- maybe daily, maybe weekly. IndexNow tells search engines that a specific page changed right now. Sitemaps are passive discovery; IndexNow is active notification. For time-sensitive product data, the difference between "Bing will find it eventually" and "Bing knows about it in five minutes" can directly impact your AI search visibility.

---

IndexNow is one piece of the AI search optimization pipeline. It handles the "get re-indexed fast" step. But fast indexing of bad data does not help. Make sure your [product data is structured correctly](/blog/shopify-agentic-storefronts-what-merchants-need-to-know/), your [GTINs are in place](/blog/gtin-ean-upc-shopify-ai-search/), and your schema markup is complete before worrying about indexing speed. Get the data right first. Then make sure the engines see it fast. That is the sequence that works.

If you want the full pipeline automated -- structured data enrichment, JSON-LD injection, GTIN mapping, and IndexNow notifications -- [Agentic Flow](https://apps.shopify.com/agentic-flow-aeo-metafields) handles all of it. Free for up to 20 products.
