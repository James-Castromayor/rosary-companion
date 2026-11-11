# Rosary Companion

Free React + TypeScript + Vite progressive web app for guided Catholic Rosary prayer.

## Run locally

1. Install Node.js 20.19+ or 22.12+.
2. In this folder run `npm install`.
3. Run `npm run dev` and open the displayed local URL.
4. Run `npm run build` to create production assets in `dist/`.

## Deploy to Cloudflare Pages (free tier)

1. Create a free GitHub repository and push these files.
2. In Cloudflare Dashboard → Workers & Pages → Create → Pages → Import an existing Git repository.
3. Build command: `npm run build`. Output directory: `dist`. Root directory: `/`.
4. Deploy. Choose an available `*.pages.dev` subdomain.
5. Cloudflare provides HTTPS. Browser installation support varies by platform and browser; on iOS use Safari → Share → Add to Home Screen.

## Structure

- `src/prayers.ts`: translations, mystery names, and Rosary sequence.
- `src/main.tsx`: prayer UI, progress, speech synthesis.
- `src/style.css`: mobile-first styles.
- `public/manifest.webmanifest`, `public/sw.js`: PWA metadata and basic offline cache.

## Important limitations

- The bead graphic highlights each decade's 10 Hail Mary beads and large beads, but is a simplified teaching diagram, not a precise traditional rosary chain. The initial opening and closing prayers are shown in text and progress indicator.
- Speech synthesis uses device voices, not recordings or chant. Latin/Filipino voices may be missing. No audio files or paid APIs are required.
- Texts are draft liturgical translations; have a Catholic reviewer check wording and regional variations before public launch.
- No account synchronization: progress is stored locally on each device.
- Basic service worker caches visited files; first use requires internet and offline behavior varies. External Google Fonts may not be available offline.
- The current mystery suggestions use the device's local day: Monday/Saturday Joyful, Tuesday/Friday Sorrowful, Wednesday/Sunday Glorious, Thursday Luminous. Seasonal Sunday variations are not implemented.
- Future church lookup should request browser geolocation consent and use a map provider that fits traffic and attribution requirements.
- Free-tier services have quotas and can change their terms; no guarantee of unlimited free hosting or email sending.


## Version 1.2 controls
- Mystery dropdown includes weekday schedule; defaults to today's mystery on every app launch (based on the device's local day).
- Listen starts continuous speech and advances automatically; Stop halts speech and automatic progression.
- Previous Mystery and Next Mystery jump to the opening Our Father of the adjacent decade, stopping audio.
- Background speech playback is not guaranteed when the device locks or the browser suspends speech synthesis.

## v1.3 changes
- Removed counterclockwise instruction text from rosary diagram.
- Extended the diagram's introductory chain to avoid overlapping beads.
- Listen speed selector: 1×, 1.25×, 1.5×, 2× (applies to subsequent prayers; stop/restart to apply immediately).
- Device voice selector filtered by prayer language; availability depends on browser and OS.
- Listen continues automatically until stopped or completed; locked-screen background playback is not guaranteed.

## Version 1.5 notes

- English playback prefers **Microsoft Sonia Online (Natural)** if the browser exposes it through `speechSynthesis.getVoices()`. If unavailable, another matching English voice is used. A previously manually selected voice remains preferred.
- While Listen is active, the app requests a Screen Wake Lock. This works only in supporting browsers over HTTPS or localhost and may be revoked by the OS. It cannot override manual screen locking or guarantee background audio.
- To deploy with GitHub + Cloudflare Pages: upload the *contents* of this folder to the repository root; build command `npm run build`, output directory `dist`, production branch `main`.
