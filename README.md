# my-tv-channels

Channel list for my personal Google TV app (MyPersonalTV).

The app downloads [`channels.json`](channels.json) every time it starts, from:

```
https://raw.githubusercontent.com/ahmad-arab/my-tv-channels/main/channels.json
```

When a stream stops working, fix its URL here. No app rebuild needed.
GitHub caches raw files for about 5 minutes, so changes may take a few minutes to show up on the TV.

## Format

```json
{
  "version": 1,
  "channels": [
    {
      "id": "rudaw",
      "name": "Rudaw",
      "group": "Kurdish",
      "urls": ["https://main-url.m3u8", "https://backup-url.m3u8"]
    }
  ]
}
```

| Field | Required | Meaning |
|---|---|---|
| `id` | yes | Unique, never changes (used to remember the last watched channel) |
| `name` | yes | Shown on the TV |
| `group` | yes | Section the channel appears in, e.g. `Kurdish`, `Arabic` |
| `urls` | yes | One or more stream URLs. The app tries them in order and uses the next one if a stream fails |
| `logo` | no | Image URL for the channel tile |
| `headers` | no | Extra HTTP headers some streams need, e.g. `{ "Referer": "https://example.com/" }` |

## Tips

- Test a new URL in **VLC** first (Media → Open Network Stream).
- Good place to find official free streams: [iptv-org/iptv](https://github.com/iptv-org/iptv/tree/master/streams) (`iq.m3u` for Iraq/Kurdistan, `qa.m3u`, `ae.m3u`, `sa.m3u` for Arabic channels).
- Check the JSON is valid before committing (a missing comma breaks the whole list), e.g. with [jsonlint.com](https://jsonlint.com).
