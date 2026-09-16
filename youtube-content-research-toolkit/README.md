# Best Apify Actors for YouTube Content Research & Repurposing

A bundle of YouTube data Actors for pulling transcripts, searching content, and profiling channels and videos at scale — the data layer behind content repurposing, competitive research, and LLM/RAG pipelines built on video content.

## Who this is for

- **Content creators & podcasters** repurposing their own or competitors' videos into blog posts, show notes, or social clips.
- **Marketers & researchers** analyzing what's working in a niche — titles, topics, upload cadence, engagement.
- **AI/LLM builders** who need transcript text as training or retrieval data instead of raw video files.
- **Localization teams** needing translated transcripts for multi-language content or subtitling.

## What's in the toolkit

| Actor | What it extracts | Link |
|---|---|---|
| Youtube Transcript Scraper | Full transcript text for a single video URL | [pintostudio/youtube-transcript-scraper](https://apify.com/pintostudio/youtube-transcript-scraper) |
| Youtube Multiple Transcript | Transcripts for a batch of video URLs in one run | [pintostudio/youtube-multiple-transcript](https://apify.com/pintostudio/youtube-multiple-transcript) |
| Youtube Translated Transcript | Transcript translated into a target language | [pintostudio/youtube-translated-transcript](https://apify.com/pintostudio/youtube-translated-transcript) |
| Youtube Search Actor | Search results for a keyword — titles, channels, view counts, links | [pintostudio/youtube-search-actor](https://apify.com/pintostudio/youtube-search-actor) |
| Youtube Video Actor | Full metadata for a single video (views, likes, description, tags, upload date) | [pintostudio/youtube-video-actor](https://apify.com/pintostudio/youtube-video-actor) |
| Youtube Channel Actor | Channel profile data (subscriber count, video list, about info) | [pintostudio/youtube-channel-actor](https://apify.com/pintostudio/youtube-channel-actor) |

## How it fits together: a repurposing pipeline

1. **Youtube Search Actor** → find the top-performing videos for a topic/keyword in your niche.
2. **Youtube Video Actor** → pull full metadata for the winners (views, engagement, upload date) to confirm they're worth repurposing.
3. **Youtube Transcript Scraper / Youtube Multiple Transcript** → pull the transcript text for those videos.
4. Feed the transcript into an LLM to generate a blog post, newsletter, or set of short-form clips.
5. **Youtube Translated Transcript** if you're localizing the output for another market.
6. **Youtube Channel Actor** on competitor channels to track their upload cadence and catalog over time.

## Code example: turn a video into a blog draft (Node.js)

```js
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });

async function runActor(slug, input) {
  const run = await client.actor(`pintostudio/${slug}`).call(input);
  const { items } = await client.dataset(run.defaultDatasetId).listItems();
  return items;
}

const videoUrl = 'https://www.youtube.com/watch?v=VIDEO_ID';

const [videoMeta] = await runActor('youtube-video-actor', { videoUrl });
const [transcript] = await runActor('youtube-transcript-scraper', { videoUrl });

console.log(`Title: ${videoMeta.title} (${videoMeta.viewCount} views)`);
console.log(`Transcript length: ${transcript.text.length} chars`);

// Pass `transcript.text` + `videoMeta` straight into your LLM prompt:
// "Turn this transcript into a 700-word blog post with the title '${videoMeta.title}'..."
```

## Batch transcripts for a whole channel (Python)

```python
from apify_client import ApifyClient
import os

client = ApifyClient(os.environ["APIFY_TOKEN"])

channel_run = client.actor("pintostudio/youtube-channel-actor").call(
    run_input={"channelUrl": "https://www.youtube.com/@examplechannel"}
)
channel_data = client.dataset(channel_run["defaultDatasetId"]).list_items().items
video_urls = [v["url"] for v in channel_data[0]["videos"][:20]]

transcripts_run = client.actor("pintostudio/youtube-multiple-transcript").call(
    run_input={"videoUrls": video_urls}
)
transcripts = client.dataset(transcripts_run["defaultDatasetId"]).list_items().items
print(f"Pulled {len(transcripts)} transcripts")
```

*(Input field names above are illustrative — check each Actor's "Input" tab on its Apify Store page for the exact schema before running.)*

## Use cases

**Content repurposing at scale.** Turn a backlog of your own videos into blog posts, LinkedIn carousels, and email newsletters by batch-pulling transcripts and feeding them to an LLM — no manual re-watching and typing.

**Competitive content research.** Use Youtube Search + Youtube Video Actor to find the highest-performing videos on a topic across the whole platform, then study titles, thumbnail patterns, and hooks that are actually working right now.

**RAG / AI knowledge base.** Feed transcripts from an educational or documentation-style channel into a vector database to build a chatbot that can answer questions "as if" it watched every video.

**Multi-language distribution.** Use Youtube Translated Transcript to get a localized script for subtitling or dubbing a video into a new market without hiring a manual translator for the first draft.

**Channel growth tracking.** Schedule Youtube Channel Actor weekly against competitor channels to track subscriber growth, upload frequency, and catalog changes over time.

## FAQ

**Can I get a YouTube transcript without opening the video?**
Yes — Youtube Transcript Scraper returns the full transcript text for any public video URL as structured JSON, and Youtube Multiple Transcript does the same for a batch of URLs in one run.

**Is there a way to get YouTube transcripts translated into another language?**
Youtube Translated Transcript returns the transcript in your chosen target language, useful for localization and subtitling workflows.

**How do I find the top-performing videos on a topic?**
Youtube Search Actor returns search results (titles, channels, view counts, links) for any keyword, which you can sort and filter by view count or upload date.

**Can this pull data for an entire channel, not just one video?**
Yes — Youtube Channel Actor returns channel-level metadata including a video list, which you can feed directly into Youtube Multiple Transcript to batch-process an entire back catalog.

**Is scraping YouTube data and transcripts allowed?**
These Actors extract publicly visible video and transcript data. Always review YouTube's terms of service and applicable law for your specific use case, particularly around redistribution of transcript text.

**Can this run automatically for new uploads?**
Yes — pair Youtube Channel Actor with Apify [scheduling](https://docs.apify.com/platform/schedules) and webhooks to detect new uploads and automatically kick off transcript and metadata pulls.

---

⬅ [Back to all toolkits](../README.md) · Explore the full data catalog at [apify.com/pintostudio](https://apify.com/pintostudio)
