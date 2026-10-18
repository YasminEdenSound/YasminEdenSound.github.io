# Editing the site

Everything on the page — every sentence, photo, price and phone number — can be
changed from one page in your browser. You never have to touch code.

**The editor lives at:** `https://yasminedensound.github.io/editor.html`

Open it on a laptop if you can. It works on a phone, but you'll be squinting.

---

## The very first time (about five minutes, once)

### 1. Open the editor

Go to the address above. It asks for a passphrase. It is **`jasmine`**.

That passphrase only keeps strangers from poking at the form. It is not what
protects the site — the token in step 2 is. Change it whenever you like:
**Settings → Passphrase for this page**.

### 2. Make a GitHub token

A token is a long password that lets the editor save files for you. Without
one you can still write and preview, but the **Publish** button won't work.

1. Sign in to GitHub, then open
   [github.com/settings/personal-access-tokens/new](https://github.com/settings/personal-access-tokens/new)
2. **Token name:** anything — `site editor` is fine.
3. **Expiration:** pick the longest you're offered. When it runs out, publishing
   stops working and you make a new one exactly this way.
4. **Repository access:** choose *Only select repositories*, then pick
   **YasminEdenSound.github.io**.
5. **Permissions → Repository permissions → Contents:** set to
   **Read and write**. Leave every other permission alone.
6. Press **Generate token** and copy the `github_pat_…` string. GitHub shows it
   once — if you lose it, just make another.
7. Back in the editor: **Settings** → paste it into **Token** → **Save**.

It's kept in that browser on that computer and sent nowhere except GitHub.
Don't do this on a shared machine. **Forget token** wipes it.

---

## Day to day

The screen is split. Left is the form, right is the **real page** — not a mock-up
of it, the actual site, redrawn about half a second after you stop typing. Click
into a field and the preview jumps to the part you're editing.

1. Open a section, change what you want.
2. Watch the right-hand side.
3. Press **Publish**.

Publishing takes a few seconds, then GitHub rebuilds the site — usually under a
minute. The top-right corner always tells you where you stand: *Published*,
*Not published yet*, or what went wrong.

If you close the tab mid-edit, your words are kept and offered back next time.
Photos you had chosen but not published are **not** kept — you'd pick those again.

---

## What's in each section

| Section | What it controls |
|---|---|
| **Site basics** | The browser tab, the Google description, your name top and bottom, and the launch switch |
| **Top menu** | The links in the bar that follows you down the page, and the *Book a session* button |
| **Opening screen** | The first thing anyone sees — headline, the line under it, the scroll hint |
| **Your story** | The scrolling chapters: words, photos, captions |
| **Selected work** | The three track cards and their audio |
| **At the desk** | The portrait, the paragraph beside it, the three facts |
| **Services & rates** | The price cards and what's included in each |
| **Book a session** | How people reach you, and where the contact form sends |

### Your story

Each chapter is one screenful. You can add, delete and reorder them with the
**↑ ↓ ✕** buttons, and the animation behind the text keeps up on its own — the
marks down the right-hand edge and the strings both count your chapters.

Give a chapter more than one photo and they stack into a fan the visitor taps
through. One photo just sits there.

Paragraphs have a **"grey this one out"** switch. That's what the `[bracketed]`
notes use — they're reminders to yourself, visible on the live site in grey.
When you've written the real thing, untick the switch or delete the paragraph.

### Photos

Press **Choose a photo…** and pick one. Anything oversized is shrunk on the way
in, so a photo straight off your phone is fine. Landscape works best — the frames
are 3:2 and a portrait photo gets cropped to fit.

A photo you've just chosen shows **"uploads on publish"**. It's only in your
browser until you press Publish.

**"What it shows"** matters more than it looks: it's what sits in the empty frame
before the photo loads, and what a blind visitor hears instead of the picture.

### Audio

Same idea — **Choose an audio file…**, pick an mp3. A card with no file shows
*Unavailable* with its play button switched off, which is what visitors see right
now for tracks 2 and 3.

The meter isn't decoration; it's reading the actual sound coming out.

---

## The launch switch

**Site basics → Keep the site hidden from Google.**

While it's on, search engines are asked to stay away, so nobody stumbles onto a
half-finished page. Turn it off when you want to be found and press Publish — it
updates the page *and* the `robots.txt` file that crawlers read.

Worth doing a sweep for `[square brackets]` before you flip it. They're the
placeholders: `[Track title]`, `[hello@example.com]`, `[20XX]`, `[Year]`, `[City]`.

---

## Two things the editor can't do for you

- **The contact form goes nowhere** until it has a real address. Make a free form
  at [formspree.io](https://formspree.io), copy the address it gives you, and paste
  it into *Book a session → Where the contact form sends*. Until then, anything a
  visitor types is lost.
- **The conservatoire logo is the wrong one.** The file sitting in chapter 2 is the
  Royal Conservatory of Music in *Toronto* — a different institution, and their
  trademark. Replace it before launch.

---

## When something looks wrong

**"I published but the site looks the same."** Give it a minute, then reload the
page properly — <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>R</kbd> (<kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>R</kbd> on a Mac). The preview in
the editor is always the truth about what you've written.

**"GitHub refused the token."** It's expired, or it was pasted wrong. Make a new
one — step 2 above.

**"The site changed since this editor loaded it."** Something else edited the
site — another tab, another device. Press **Reload from site**, make your change
again, publish.

**I've broken something and I don't know what.** Nothing is ever lost: every
publish is a saved version in GitHub, and any of them can be put back. Say the
word and it gets restored.

**I'd rather not publish from here.** Settings has **Download content.js** and
**Download new photos / audio**. Send those on and someone else can put them in.

---

## For whoever maintains this

- `content.js` — every editable string, photo path and number, as JSON. The only
  file the editor rewrites in normal use.
- `index.html` — unchanged in spirit: the copy is still written out in the markup,
  and a small script at the foot of the page copies `content.js` over it before the
  main script runs. If `content.js` ever fails to load, the page renders the baked-in
  copy instead of breaking.
- `editor.html` — the form. Pure client-side; talks to the GitHub Contents API with
  a token held in `localStorage`.
- The preview is `index.html?preview=1` in an iframe, reading the draft from
  `localStorage`. The live site never looks at that.
- Uploaded files get a unique filename rather than overwriting — GitHub Pages
  caches by URL, so reusing a path serves the old image for ten minutes. The cost
  is that replaced files stay in the repo; prune them by hand if it ever matters.
- The launch switch rewrites `robots.txt` and one marked line in `index.html`
  (`<!-- ye-robots -->`). Leave that marker alone.
- The passphrase is a SHA-256 hash on the line marked `/* ye-pass-hash */`.
  Obscurity, not security — the token is the thing that matters.
