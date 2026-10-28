# Niv's Page 🌈

A single-page website for Niv, in Hebrew, made for a kiosk tablet. No build step and no dependencies to install.

- 🎧 **Music!**: once a parent has connected Spotify, opens a simple music screen with big picture tiles and giant ⏮ ▶/⏸ ⏭ buttons. The page remote-controls the Spotify app running in the background on the same tablet, so Niv never sees Spotify's own screens. Before Spotify is connected, the button just opens the Spotify app.
- 💖 **Mom's page**: opens [Niv's page from mom](https://malissshany-cpu.github.io/family-hub/index.html).

## Files

- `index.html`: Niv's page, including the music screen and the parent panel.
- `setup.html`: the parent's phone page for connecting Spotify and choosing tiles.

## Connecting Spotify

Needs Spotify Premium (Spotify only lets apps control playback for Premium accounts).

1. Create an app at the [Spotify developer dashboard](https://developer.spotify.com/dashboard), choosing **Web API**, with redirect URI `https://sergeipr.github.io/kidsbits/setup.html`. Under **User management**, add the Spotify account the tablet plays from.
2. Put the app's Client ID in `CLIENT_ID` at the top of the script in `setup.html` (it isn't secret).
3. On the tablet, hold the **היי ניב** title for two seconds, then tap **Connect with phone**.
4. Scan the QR code with your phone, sign in to Spotify, pick the tiles, and tap **Send to tablet**.

The phone sends the Spotify sign-in and the tile list to the tablet through a one-time [ntfy.sh](https://ntfy.sh) topic, encrypted with a key that only exists inside the QR code. Spotify asks for a new sign-in about every six months; the music screen then says a parent needs to reconnect, and you repeat steps 3–4. Repeat them any time to change the tiles.

The Spotify app has to be running on the tablet. If Android has stopped it, the music screen shows a button that opens it; press 🏠 or Home to come back.

## Run it

Serve the folder with any static server (for example `python3 -m http.server`) and open `index.html`. To host it, enable GitHub Pages on this repo.
