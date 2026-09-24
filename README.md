# The public page

Three forms want a URL before ROT FACTORY can be submitted anywhere, and one page answers all of them:

| Asked by | Field | URL |
|---|---|---|
| AppLovin MAX sign-up | Website | `https://<user>.github.io/rotfactory/` |
| Google Play + App Store Connect | Privacy policy | `https://<user>.github.io/rotfactory/privacy.html` |
| Google Play | Support URL | `https://<user>.github.io/rotfactory/` |

Two files, no build step, no Jekyll: `index.html` (the game, and where to write for help) and `privacy.html`.

## Who it says it is

Filled in on 2026-09-24 and checked against the rest of the project, because three places have to agree:

| | |
|---|---|
| Support address | `tolga_nacar@outlook.com` — also the support email on both store listings |
| Developer name | `Tolga Nacar` — also `PlayerSettings.companyName`, the AppLovin account's Company, and the developer name in Play Console and App Store Connect |

Changing either means changing it in all of those at once: the stores check the name against the entity
that signed the agreements, and a support address that bounces is a review rejection.

## Putting it online

The game's own repository is **private**, and GitHub Pages does not serve private repositories on the free
plan. Making it public is not an option before launch — the art, the content table and the merge rules are
the game (`docs/SECURITY.md`). So the page is served from a second, public repository that holds nothing
but these files.

This folder stays the one source of truth: it is versioned with the game, so a change to an SDK and the
change to the policy that describes it land in the same commit. The public repository is fed from it with
`git subtree`, not with a `git init` in here — a repository nested inside a tracked folder is a mess that
only shows up later.

Once, to set it up:

```sh
# On github.com: New repository > name "rotfactory" > Public > no README, no .gitignore > Create.
cd /Users/tolganacar/Desktop/rot-factory
git remote add site git@github.com:tolganacar/rotfactory.git
git subtree push --prefix site site main
# On github.com: Settings > Pages > Source "Deploy from a branch", branch "main", folder "/ (root)".
```

Live a minute later at `https://tolganacar.github.io/rotfactory/`. Check that `privacy.html` opens
directly: store reviewers paste that exact URL, and a policy behind a redirect or a login is a rejection.

Afterwards, to publish a change:

```sh
git subtree push --prefix site site main
```

## Keeping it honest

The privacy policy describes what the game actually ships with — Firebase Analytics, Crashlytics, AppLovin
MAX, Unity IAP, Game Center and Play Games. **If an SDK is added or removed, this page changes in the same
commit**, and so does the Data safety form in Play Console. A policy that disagrees with the SDKs in the
binary is what Google's reviewers look for.

It also states the game is **not directed at children under 13**. That has to match the answer given in
Play Console's target-audience form; the two are checked against each other.
