DROP YOUR MEDIA IN THIS FOLDER.

Every path in index.html resolves to ./assets/, so these files sit right here
next to index.html when deployed. Any file that is missing renders a branded
placeholder naming it — the layout stays intact while you gather media.

Filenames are case-sensitive once deployed. "Origin-DFW.jpg" will 404 on
Cloudflare Pages even though it works locally on macOS.

────────────────────────────────────────────────────────────────────────────
IMAGES
────────────────────────────────────────────────────────────────────────────

  origin-dfw.jpg        DFW departure — landscape, 16:9 or wider
  destination-syd.jpg   Sydney arrival — landscape, 16:9 or wider
  cabin-a380.jpg        A380 cabin at cruise — the film treatment frame
  creator-profile.jpg   Creator portrait — 4:3 crop reads best

  Target ~1800-2400px on the long edge, under ~600KB each.

  NOTE ON THE FIRST THREE: they carry the caption
  "TREATMENT REFERENCE · DIRECTION, NOT FINAL FRAMES" in the layout, because
  they are direction, not portfolio. Do not swap that caption off unless the
  images become your own frames from an actual Qantas shoot.

  If you switch the deck to the SFO preset (see the main README), add:
  origin-sfo.jpg

────────────────────────────────────────────────────────────────────────────
VIDEO — the Selected Work cards
────────────────────────────────────────────────────────────────────────────

  work-reach.mp4  + work-reach.jpg   REACH  13M IG / 8.3M TikTok
  work-craft.mp4  + work-craft.jpg   CRAFT  2.3M IG
  work-brand.mp4  + work-brand.jpg   BRAND  1.5M IG — The Edge collaboration
                                     (this is the reel at instagram.com/reel/
                                     DUPNomqkVsW — export that one)

  The .jpg alongside each is the poster frame shown before playback.

  These are SELF-HOSTED ON PURPOSE. The older decks in this repo use
  Instagram embeds; those are blocked on most corporate networks and this
  proposal is built to be forwarded inside Qantas. Do not swap them back.

  Export 9:16, H.264/AAC, ~1080x1920, and keep each file under ~8MB —
  they are set to preload only when scrolled into view, but four people
  opening this on hotel wifi should still not wait.
