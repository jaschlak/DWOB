# DWOB Practice Library

Static, phone-friendly rhythm video library for `jordanschlak.com/dwob`.

GitHub repository:

```text
git@github.com:jaschlak/DWOB.git
```

## Cheapest hosting recommendation

Use a static host and keep the actual video files on YouTube, Vimeo, or another video platform. Do not host raw video files in this repo unless you want bandwidth, storage, transcoding, and mobile playback costs.

Good cheap options:

- GitHub Pages: free for public repositories, supports custom domains, and is enough for a simple static site.
- Cloudflare Pages: free tier includes Git integration, custom domains, unlimited static requests, and unlimited bandwidth.
- AWS CloudFront + S3: good if you want to keep it inside AWS. AWS currently advertises a $0/month CloudFront free plan with 5 GB included S3 storage, 1M requests, and 100 GB data transfer.

Kubernetes is not the cheapest production choice for this site. The included `Dockerfile` and `k8s/deployment.yaml` are useful for learning or for running this as a container, but static hosting is simpler and cheaper.

## Edit the video list

Update `videos.json`:

```json
{
  "title": "Warmup Groove",
  "description": "A short pocket-building loop for getting hands and feet moving.",
  "youtubeId": "YOUTUBE_VIDEO_ID",
  "level": "beginner",
  "tempo": "90 BPM",
  "duration": "3:33"
}
```

For a YouTube URL like:

```text
https://www.youtube.com/watch?v=abc123XYZ00
```

the `youtubeId` is:

```text
abc123XYZ00
```

## Run locally

Because the app fetches `videos.json`, serve it with a tiny web server:

```powershell
python -m http.server 8080
```

Then open:

```text
http://localhost:8080
```

## Run with Docker

```powershell
docker build -t dwob-site .
docker run --rm -p 8080:80 dwob-site
```

## Deploy path

Recommended first deploy:

1. Push this repository to `git@github.com:jaschlak/DWOB.git`.
2. In GitHub, open Settings -> Pages.
3. Set Build and deployment -> Source to GitHub Actions.
4. Push to `main`.
5. The workflow in `.github/workflows/pages.yml` will publish the site.

GitHub Pages project URL:

```text
https://jaschlak.github.io/DWOB/
```

For `jordanschlak.com/dwob`, use Cloudflare Pages or CloudFront routing in front of the GitHub Pages URL, or host the built static files directly on Cloudflare Pages/AWS with that path configured.
