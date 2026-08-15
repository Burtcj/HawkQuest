# Hawk Quest — Corkscrew Middle School

Everything in this folder is the site. Drop it in a GitHub repo, turn on Pages,
and the link works.

## Files

| File | What it is |
|---|---|
| `index.html` | Hawk Quest. This is the student link. |
| `flight.html` | Hawk Flight on its own, if you ever want it separately. |
| `preview.html` | Same game with the weekend window and play limit switched off, for testing. **Do not give this to students.** |
| `assets/title-music.mp3` | Plays on the title screen only. |
| `.nojekyll` | Tells GitHub to serve the files as-is. Leave it there. |

## Putting it on GitHub Pages

1. On github.com, **New repository**. Name it `hawkquest`. Public. Create.
2. On the repo page, **Add file → Upload files**. Drag in `index.html`,
   `flight.html`, `preview.html`, `.nojekyll`, and the whole `assets` folder.
   Commit.
3. **Settings → Pages.** Under *Build and deployment*, Source = **Deploy from a
   branch**, Branch = **main**, folder = **/ (root)**. Save.
4. Wait a minute or two. Your link is:

       https://burtcj.github.io/hawkquest/

   5. Open that link and check the title screen loads and the music starts when you
   tap.

## Before it goes to students

- **Put the real link in three places:** the Canvas ad, the flier, and slide 31
  of the Hawk Expectations deck. All three already read `burtcj.github.io/hawkquest`.
- **The Microsoft Form needs a grade-level question**, or the codes cannot be
  sorted into the three drawings.
- **The form also needs a 1st period teacher and 7th period teacher field**
  (dropdowns, not free text) for the teacher prize. The score code no longer
  carries a period.
- **Update your Hawk Code Reader.** Codes now read `HAWK-<initials>-XXXX-XXXXX`
  with no period digit, and the checksum covers the initials only. Reader needs
  the period digit removed from the prefix and from `identVal`.


## The secret in the cafeteria

There is an unmarked tile in the far corner of B lunch, past the trash cans.
Nothing on the map points at it. A student who wanders over there meets
**Hawkman** and can try to catch him: calm him down first (talk to him, hold
still, offer a Hawk Dollar), then reach out. Grab too early and he shrugs you
off. One encounter per run.

Catch him and the score code comes out as **HAWKMAN-JB-XXXX-XXXXX** instead of
**HAWK-JB-XXXX-XXXXX**, so you can spot it at a glance in the form responses.

**Your Hawk Code Reader needs to know about this**, or those codes will fail to
verify. Two changes:

- accept `HAWKMAN` as well as `HAWK` at the front of the code
- when the prefix is `HAWKMAN`, add 17 to the checksum sum before taking `% 31`

That second part is deliberate. It means a student who just types HAWKMAN over
the front of an ordinary code fails verification.

## Changing the play window

Near the top of the `<script>` in `index.html`:

    const OPEN_AT  = new Date(2026,7,21,15,50,0);   // Fri Aug 21 2026, 3:50 p.m.
    const CLOSE_AT = new Date(2026,7,24, 8,30,0);   // Mon Aug 24 2026, 8:30 a.m.

Months count from zero, so `7` is August. The two `WHEN_OPEN` / `WHEN_CLOSE`
lines just below are the wording students see — change those to match.

The window is checked against the clock on the **web server**, not the student's
device, so a student changing the clock on their phone gets nowhere. That check
needs the page to be online: if it cannot reach the server it will not open, which
is deliberate — it stops a student saving the file and playing it offline later.

## Teacher link

Add `?teacher` to the end of the address:

    https://burtcj.github.io/hawkquest/?teacher

That skips the weekend window and turns on the skip keys —
`]` jumps to the next stage, `\` jumps to the end.
