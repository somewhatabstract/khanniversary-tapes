# The Khanniversary Tapes

A single-page static site (`index.html`) celebrating Jeff's 9th khanniversary
at Khan Academy: nine five-song YouTube playlists ("tapes") drawn from almost a
year of weekly original live song demos, presented as CSS-drawn cassette tapes.
Deployed via GitHub Pages (Settings → Pages → deploy from branch → `main` /
root) at <https://somewhatabstract.github.io/khanniversary-tapes/>.

## Design language (decided, do not casually revisit)

- **Committed dark "studio" theme** — same in every mode; the light theme was
  deliberately removed. Deep blue-black ground (`#14161c`), amber tube-glow
  accent (`#f0a828`).
- **Cassette skeuomorphism**: each tape is a shell with corner screws,
  write-protect notches, a plastic sheen, a Memorex-style white label sticker
  (faint blue ruled lines, curator colour band, marker-pen title in
  'Permanent Marker' from Google Fonts with wavy underline, faint biro
  "C-90 · HIGH BIAS" stamp, quiet biro "Open playlist on YouTube" link), a
  tape window BETWEEN two spoked reels (uneven tape pack: left fuller), and
  a trapezoid baseplate. Reels shrink, never vanish, on small screens.
- **Tracklist-first windows**: each window rests as a paper J-card insert
  showing the playlist's tracklist (fetched client-side from the YouTube
  Data API v3; key in-page, referrer-restricted to the Pages origin and
  API-restricted to YouTube Data — safe to be public) plus an amber play
  button. Pressing play creates the embed on demand (autoplay=1) and the
  card rotates up like a lid; no YouTube iframes load before that.
  Fallback copy: empty playlist → "this side hasn't been recorded yet";
  API unreachable (incl. non-Pages origins — the referrer restriction 403s
  everywhere else) → "label unreadable — press play and find out".
  `<noscript>` keeps plain embeds for JS-less visitors. After the card
  slides away a paper "TRACKS" tab peeks from the window's right edge and
  slides it back in over the playing video, with the current track under a
  highlighter-pen sweep (IFrame API playlist index). Embeds use `rel=0`
  (related videos still appear, but only from the same channel).
- **Reels spin only during playback** (YouTube IFrame API state events),
  counter-clockwise like a cassette playing side A; the sheen (two passes,
  different speeds) sweeps across each shell on scroll. Interaction
  rewards, not ambient motion.
- **Easter eggs** (all deliberate, all quiet): tape packs wind from left
  reel to right as the playlist progresses (`--wind` from the playlist
  index); the playing tape's nav mini-cassette tooltip spins its reels;
  the hero VU meter runs hot while anything plays (`vu-live` on body);
  tape 05's write-protect tab is punched out (nobody records over the
  creator's cut); loading a DIFFERENT tape into the deck plays a real
  cassette-insertion recording (inlined base64 MP3, trimmed, from
  orangefreesounds.com under CC BY-NC 4.0 — credited in the liner notes;
  the video load waits for it). Same-tape resume/reveal is silent. The
  tracklist deliberately keeps playing when slid over the video: playback
  started user-visible and the card carries its own pause control. The
  playing tape's nav button carries a mini VU meter in its track colour;
  ejected tapes rewind (re-cued to track 1, highlight and winding
  cleared); tracklist rows are click/keyboard playable (playVideoAt,
  with the swap sound when it's a different tape).
- **Nav** is a tape-deck preset row: numbered buttons with full playlist names,
  clickable "A ▸ / B ▸" side links, a vertical separator, then "✱ Outro" and
  "∞ Full list ↗" (external). Mini-cassette CSS tooltips on hover carry short
  enticement blurbs; a small script clamps tooltips at viewport edges.
  Below 620px buttons collapse to numbers only.
- **VU meter** flourish spans the full hero width (56 flex bars).
- Animations respect `prefers-reduced-motion` (reels + VU freeze).
- **British English** throughout the copy (`lang="en-GB"`); CSS keywords stay
  as-spec. Jeff is British-American; 90s BritPop mixtape vibes welcome.

## Content structure

- Hero: "The Khanniversary Tapes", "nine tapes for nine years", quiet inline
  link to the full collection
  (<https://www.youtube.com/playlist?list=PLp_aNQTHQdJiJa1GwaummT-Z762FW242C>).
- **Side A · picked by people** (01–05): Dave's Deep Cuts, Matthew's Mixtape,
  Walt's Wavelengths, Eric's Earworms, Jeff's Jams (Jeff's own; "the
  creator's cut" lives in its blurb; closes side A deliberately).
- **Side B · picked by numbers** (06–09): Claude's Chorus (picked from Slack
  interactions), Gemini's Gems (most-viewed — skews Shorts, known and
  accepted), The Long Plays (most-watched full-length, non-Short videos;
  includes talent-show entries), Hidden Tracks (least-viewed; closes the page
  on purpose — "the overlooked get the last word").
- Outro liner notes: thanks to the four human curators and Khan Academy;
  encouragement to create ("...only you could make"); credit line "first
  pressing by Gemini · remastered with Claude"; sign-off "Recorded live, one
  take at a time".
- `noindex, nofollow` is intentional: the page is public-but-link-only.

## Known follow-ups

- **Playlist IDs to verify on the live site**: Dave's (`PLafgqXA6oHhU`) and
  Matthew's (`PLb6R968zXD5M`) came from an earlier Gemini draft and look
  truncated (real IDs are ~34 chars). All others were supplied by Jeff
  directly but are also short-looking — verify every embed loads.
- Jeff's Jams (`PLMjdH71empG0`) and Eric's Earworms (`PLbvqrSnnG-9s`)
  playlists exist but were empty at launch; videos to be added. Jeff's Jams
  will carry NINE tracks, not five — the creator's cut, one per year; the
  blurb owns the rule-break and long tracklists (6+) render tighter. The
  tracklist fetch caps at `maxResults=10`; an eleventh track would silently
  drop.
- **Possible tenth list** from a colleague who hasn't responded yet. If it
  arrives: it joins Side A (making six human tapes), and Hidden Tracks becomes
  an actual hidden track / easter egg — revealed by clicking something
  on-theme (e.g. the "Recorded live, one take at a time" sign-off), keeping
  nine visible tapes for nine years.

## Working conventions

- The page is one self-contained `index.html`; keep it that way (inline CSS/JS,
  no build step). External dependencies: Google Fonts, YouTube (embeds +
  IFrame API), and the YouTube Data API (tracklists).
- During design iteration this page was previewed as a Claude artifact where
  YouTube embeds cannot load (CSP) — embeds only work on the deployed site.
