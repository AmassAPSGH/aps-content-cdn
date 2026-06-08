# APS Content CDN

Public-URL host for APS social content (PNG stills, MP4 reels).

Used by `tools/buffer_push.py` to give the Buffer API publicly-fetchable URLs for media.

## Layout

- `stills/` — final 1080x1080 still posts
- `reels/` — final 1080x1920 vertical Reels

## URL pattern

```
https://raw.githubusercontent.com/AmassAPSGH/aps-content-cdn/main/stills/<bucket>/<filename>.png
https://raw.githubusercontent.com/AmassAPSGH/aps-content-cdn/main/reels/<bucket>/<filename>.mp4
```

## Workflow

`buffer_push.py` handles all pushes automatically:

1. Copies the final media file into `stills/<bucket>/` or `reels/<bucket>/`
2. `git add` + `git commit` + `git push origin main`
3. Builds the raw.githubusercontent.com URL
4. Calls Buffer's GraphQL `createPost` mutation with that URL

Manual pushes should not be necessary.
