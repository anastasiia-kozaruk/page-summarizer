## What does Page Summarizer do?

**Page Summarizer** takes the URL of any web page, downloads it, and uses **Claude** (Anthropic's AI model) to write a **3–5 bullet summary**. Because it runs on the [Apify platform](https://apify.com), you can start it from the API, run it on a schedule, or connect it to Make, Zapier, or n8n.

## Why use Page Summarizer?

- **Save reading time:** get the gist of long articles, docs, or company pages in seconds.
- **Monitor pages:** schedule it to summarize a news or changelog page every day.
- **Feed other tools:** send the summaries to Slack, Google Sheets, or your CRM with Apify integrations.

## How to use Page Summarizer

1. Open the **Input** tab.
2. Paste the page address into **Page URL**.
3. Paste your **Anthropic API key** (get one at https://console.anthropic.com/settings/keys).
4. Optionally pick a **Claude model**.
5. Click **Start** and open the **Output** tab when the run finishes (usually under 30 seconds).

## Input

| Field   | Type              | Description                                                                |
| ------- | ----------------- | -------------------------------------------------------------------------- |
| `url`   | string (required) | The web page to summarize.                                                 |
| `model` | string            | `claude-haiku-4-5-20251001` (default, fast) or `claude-sonnet-5` (better). |

```json
{ "url": "https://apify.com/about" }
```

## Output

Each run saves one item to the dataset. You can download the dataset in various formats such as JSON, HTML, CSV, or Excel.

```json
{
    "url": "https://apify.com/about",
    "title": "About · Apify",
    "summary": "• Apify is a web data platform founded in 2015...\n• ...",
    "model": "claude-haiku-4-5-20251001"
}
```

| Field     | Description                            |
| --------- | -------------------------------------- |
| `url`     | The page that was summarized           |
| `title`   | The page's `<title>`                   |
| `summary` | Bullet-point summary written by Claude |
| `model`   | Claude model used                      |

## How much does it cost?

Each run uses a small amount of Apify compute (a few seconds) plus one Claude API call, billed to your own Anthropic API key. Haiku 4.5 is the cheapest option.

## Tips and limitations

- The Actor reads the page's raw HTML, so pages that build their content with JavaScript may give poor results.
- Very long pages are cut to the first 50,000 characters.

## Setup (for developers)

Each user enters their own Claude API key in the **Anthropic API key** input field. The field is marked `isSecret`, so Apify stores it encrypted and never shows it in logs. For local runs, the Actor falls back to the `ANTHROPIC_API_KEY` environment variable, which `.actor/actor.json` maps to the Apify secret `anthropicApiKey`.

## FAQ

**Is it legal?** It only reads publicly available pages you point it at. Respect each site's terms of service.

**Found a bug?** Open an issue in the **Issues** tab.
