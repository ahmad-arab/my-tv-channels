# my-tv-channels

Channel list for my personal Google TV app (MyPersonalTV).

The app downloads [`channels.json`](channels.json) every time it starts, from:

```
https://raw.githubusercontent.com/ahmad-arab/my-tv-channels/main/channels.json
```

When a stream stops working, fix its URL here. No app rebuild needed; the change shows up the next time the app starts.

## Format (version 2)

```json
{
  "version": 2,
  "groups": [
    { "id": "kurdish", "name": "Kurdish" },
    { "id": "news", "name": "News" }
  ],
  "channels": [
    {
      "id": "rudaw",
      "name": "Rudaw",
      "logo": "https://example.com/rudaw.png",
      "groups": ["kurdish", "news"],
      "urls": ["https://main-url.m3u8", "https://backup-url.m3u8"]
    }
  ]
}
```

### Groups

| Field | Meaning |
|---|---|
| `id` | Unique, used by channels to refer to the group |
| `name` | Shown in the app's side menu |

The side menu shows groups in this order (after Search, Favorites and All channels). Groups with no channels are hidden.
Known ids get a matching icon: `kurdish`, `arabic`, `english`, `syrian`, `news`, `documentary`, `movies`, `entertainment`, `kids`, `sports`, `religious`, `music`.

### Channels

| Field | Required | Meaning |
|---|---|---|
| `id` | yes | Unique, never changes (favorites and the last watched channel are stored by id) |
| `name` | yes | Shown on the TV and used by search |
| `groups` | yes | Ids of the groups the channel appears in; a channel can be in several |
| `urls` | yes | One or more stream URLs. The app tries them in order and uses the next one if a stream fails |
| `logo` | no | PNG/JPG image URL (SVG is not supported). Without it, the channel's initials are shown |

## Tips

- Test a new URL in **VLC** first (Media → Open Network Stream).
- Only add official, free streams. Re-broadcasts of paid channels (beIN, OSN, HBO, Sky Sports, ...) are illegal and break all the time.
- `http://` streams work too (some regional broadcasters still use plain http).
- Streams that need special HTTP headers (Referer, User-Agent) are not supported by the app.
- Good place to find streams and logos: [iptv-org/iptv](https://github.com/iptv-org/iptv/tree/master/streams) and its [API](https://github.com/iptv-org/api) (`logos.json`), plus [Free-TV/IPTV](https://github.com/Free-TV/IPTV) (curated legal channels by country).
- Check the JSON is valid before committing (a missing comma breaks the whole list), e.g. with [jsonlint.com](https://jsonlint.com).
