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
  `<noscript>` keeps plain embeds for JS-less visitors.
- **Reels spin only during playback** (YouTube IFrame API state events);
  the sheen sweeps across each shell on scroll. Both interaction rewards,
  not ambient motion.
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
  Walt's Wavelengths, Eric's Earworms, Jeff's Jams · The Creator's Cut
  (Jeff's own; shortened to "Jeff's Jams" in the nav; closes side A
  deliberately).
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
  playlists exist but were empty at launch; videos to be added.
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
