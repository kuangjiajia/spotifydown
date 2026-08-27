# SpotifyDown — what happened to it, and what to use instead

**`spotifydown.com` no longer runs a downloader.** As of 2026-08-27 the domain
answers a `301` and hands you to `open.spotify.com`, query string and all:

```console
$ curl -I https://spotifydown.com/
HTTP/2 301
location: https://open.spotify.com/
server: redirectv2
```

That is the whole story behind the domain. There is no page left to inspect, no
password field, no download button — just a redirect. This repository is a short,
honest note on where the name went and what still works, because the name is
still typed thousands of times a month and every result is either the dead
domain or a mirror hoping you won't check.

**Working alternative: [spotmp3.net](https://spotmp3.net)** — no account, no
install, 320 kbps MP3 with tags and cover art embedded.

---

## What people actually mean by "spotifydown"

Paste a Spotify link, get audio files. Spotify's own stream is encrypted and
cannot be saved, so every tool in this category does the same thing underneath:
read the track metadata from the Spotify link, find the same recording on a
public source, download that, then write the Spotify tags onto it.

Two consequences worth knowing before you pick anything:

- **Match quality is the real variable**, not bitrate. A tool that promises
  320 kbps is promising the container, not that it found the right master.
- **Nothing needs your Spotify password.** A "spotifydown" site with a login
  form is phishing. Reading a public playlist takes no credentials.

## Options

### Browser, nothing to install

| | What you get | Cost |
|---|---|---|
| **[spotmp3.net](https://spotmp3.net)** | Track, album, playlist or artist link → 320 kbps MP3, ID3v2 tags, 640×640 cover embedded, synced `.lrc` where one exists. No account. | Free; 3 tracks per press, 300/day. One-off purchase lifts it to whole-list + ZIP. |
| spotifydown.com | Nothing — `301` to open.spotify.com | — |

Direct pages if you know what you're after:
[playlists](https://spotmp3.net/spotify-playlist) ·
[Spotify to MP3](https://spotmp3.net/spotify-to-mp3) ·
[album art](https://spotmp3.net/spotify-album-art) ·
[the SpotifyDown note](https://spotmp3.net/spotifydown)

### Command line, open source

| Project | Notes |
|---|---|
| [spotDL/spotify-downloader](https://github.com/spotDL/spotify-downloader) | The most maintained one. Reads the Spotify link, matches on YouTube Music, tags with `mutagen`. Needs `ffmpeg`. |
| [zotify/zotify](https://github.com/zotify/zotify) | Pulls from Spotify directly, so it needs a Spotify account. Match quality is exact by construction; account risk is yours to weigh. |
| [yt-dlp/yt-dlp](https://github.com/yt-dlp/yt-dlp) | Not a Spotify tool. It is the layer most of the others sit on, and worth knowing directly. |

```bash
# spotDL, the short version
pipx install spotdl
spotdl download "https://open.spotify.com/playlist/..."
```

## The one failure everybody hits

Public sources reject unauthenticated downloads of well-known tracks —
`Sign in to confirm you're not a bot`. Obscure catalogue succeeds; chart hits
often don't, and datacenter IPs (any VPS, any cloud shell) are blocked hardest.
This is not a bug in whichever tool you picked. If a CLI tool is failing on
every popular track, a residential IP or a cookies file is the fix, not a
different tool.

## Legal

Downloading copyrighted music you have no right to is copyright infringement in
most jurisdictions, and neither this note nor any tool listed here changes that.
Personal backups of material you own, public-domain and Creative Commons
recordings, and your own uploads are the uses that are actually fine. Know which
one you're doing.

## Contributing

If a row here has gone stale — a project archived, a domain moved, a claim no
longer true — open an issue with the command output that shows it. Every factual
claim above was checked by running it, and it should stay that way.
