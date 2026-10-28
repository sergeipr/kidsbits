# Niv's Page 🌈

A single-page website for Niv, in Hebrew, made for a kiosk tablet. No build step and no dependencies to install.

- 🎧 **Music!**: once Spotify is connected, opens a simple music screen with big picture tiles and giant ⏮ ▶/⏸ ⏭ buttons. The page remote-controls the Spotify app running in the background on the same tablet, so Niv never sees Spotify's own screens. Podcast tiles open a list of episodes. Before Spotify is connected, the button just opens the Spotify app.
- 💖 **Mom's page**: opens [Niv's page from mom](https://malissshany-cpu.github.io/family-hub/index.html).

## Files

- `index.html`: Niv's page, with the music screen and a parent panel.
- `setup.html`: the parents' phone page for managing the tablet.

## Managing the tablet (parents)

Open the manage page on your phone from the tablet: hold the **היי ניב** title for two seconds and scan the QR code. Add the page to your home screen; from then on you can manage the tablet from anywhere, as long as the tablet is on and online. Both parents can use the same link.

On the manage page you can:

- **Add tiles** by pasting a Spotify link (in Spotify: **⋯ → Share → Copy link**): playlists, albums, artists, podcasts or single episodes. Rename, reorder or remove tiles, then **Save to tablet**.
- **Pick from your own Spotify**: sign in to list your playlists and followed podcasts and add them as tiles. That sign-in stays on your phone.
- **Connect the tablet's Spotify account**: sign in with the account the tablet should play from (it needs Premium) and tap **Use this account on the tablet**. Spotify asks for this again about every six months; the manage page shows how many days are left, and Niv's music screen says when a parent needs to reconnect.
- **See the tablet's status**: whether it's online, which Spotify account it uses, whether the Spotify app is running, and the last problem it hit.

Anyone with the manage link can manage the tablet's music, so only share it with family. The tablet's parent panel has **New link**, which stops all old links from working.

## Spotify developer app

The pages need a (free) Spotify developer app, because Spotify only lets apps control playback through one. Its owner needs Spotify Premium.

1. Create an app at the [Spotify developer dashboard](https://developer.spotify.com/dashboard), choosing **Web API**, with redirect URI `https://sergeipr.github.io/kidsbits/setup.html`.
2. Under **User management**, add every Spotify account that will sign in on the manage page (up to five).
3. The first time anyone signs in on the manage page, it asks for the app's **Client ID** and passes it to the tablet; after that, every phone gets it from the tablet. It isn't stored in this repo.

## How it works

The manage page and the tablet talk through a private [ntfy.sh](https://ntfy.sh) topic, a free public message relay. Every message is encrypted with a key that only exists on the tablet and in the manage link, so ntfy.sh only sees ciphertext. The Spotify sign-in is additionally encrypted for the tablet alone (ECDH with a key pair that never leaves it), so even someone with the manage link can't read it, and the tablet never sends it back out.

The Spotify app has to be running on the tablet. If Android has stopped it, the music screen shows a button that opens it; press 🏠 or Home to come back.

## Run it

Serve the folder with any static server (for example `python3 -m http.server`) and open `index.html`. To host it, enable GitHub Pages on this repo.
