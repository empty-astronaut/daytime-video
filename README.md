# Daytime Video

A sunny random movie picker. Set your picks, hit **Pick My Movie!**, and the shelf hands you something good. No horror on these shelves; that's what [Midnight Video](https://empty-astronaut.github.io/midnight-video/) is for.

**Live site:** `https://empty-astronaut.github.io/daytime-video/`

## What it does

Pick your limits first, then let the shelf decide:

- **Quick vibes:** one-tap presets like Family night, Date night, Popcorn, Rainy Sunday, Oldies, Short & sweet, and Certified great
- **Rated up to:** cap the MPAA rating at G, PG, PG-13 or R. Unrated classics from before the ratings system count as PG.
- **Release years:** set an earliest and latest year
- **IMDb rating:** only films at or above a minimum score
- **Runtime:** cap how long the movie can run
- **Genres:** 24 to choose from (comedy, action, animation, musical, western, heist, road trip, holiday, documentary, and more). Match **Any** of the ones you pick, or require **All** of them.
- **Skip seen:** mark films as seen and leave them out of future picks

A live counter shows how many tapes match. If nothing matches, the shelf tells you to loosen up.

Each pick shows the IMDb rating, MPAA rating, year, runtime, director, genre tags and a one-line synopsis, with links to IMDb and JustWatch. There's a short history of your earlier picks, a cheerful chime and confetti on each pick (toggle sound off in the header), drifting clouds and a spinning sun. Animations switch off automatically if your system is set to reduce motion.

## The movie list

The list is built into the page: 1,814 films from 1924 to 2025, across comedy, action, animation, drama, romance, sci-fi, musicals, westerns, documentaries and the rest. It isn't pulled from IMDb live. IMDb has no free public API, and a static page can't call most third-party APIs without exposing a key.

Ratings are approximate IMDb scores and drift over time. Use the IMDb link on each pick to see the current number.

## Run it

It's one static file with no build step and no dependencies to install.

- **Locally:** open `index.html` in a browser.
- **GitHub Pages:** go to **Settings > Pages**, set **Source** to "Deploy from a branch", choose your main branch and the `/ (root)` folder, and save. The file must be named `index.html` and sit at the top level of the repo.

Fonts (Lilita One, Nunito, Space Mono) load from Google Fonts, so the page needs an internet connection to look right.

## Add or edit movies

All the films live in one block near the top of the script in `index.html`, in a constant called `RAW`. Each film is one line with eight fields separated by pipes:

```
Title|Year|Rating|Runtime|MPAA|tags|Director|Logline
```

For example:

```
The Princess Bride|1987|8.0|98|PG|adventure,comedy,romance,fantasy|Rob Reiner|Fencing, fighting, torture, revenge, giants, monsters, true love.
```

Rules:

- Runtime is in minutes. Rating is a number like `7.4`.
- MPAA is one of `G`, `PG`, `PG-13`, `R` or `NR` (unrated; treated as PG by the filter).
- Tags are comma-separated with no spaces. Use only these keys: `comedy`, `action`, `adventure`, `animation`, `family`, `romance`, `drama`, `scifi`, `fantasy`, `thriller`, `mystery`, `crime`, `musical`, `western`, `war`, `sports`, `biography`, `history`, `superhero`, `heist`, `roadtrip`, `comingofage`, `holiday`, `documentary`.
- Don't use a `|` or a backtick inside a field.
- Skip any title and year that's already in the list, so a film doesn't show up twice.
- The year slider range adjusts on its own to the oldest and newest films.

Commit the change and GitHub Pages redeploys in a minute or two.

## Saved in your browser

Your filters, seen list, pick history and sound setting are saved with `localStorage`, so they stick around between visits on the same browser and device. Nothing is sent anywhere. Clearing site data resets them, and the **Reset picks** button restores the default filters.

## Credits

Built with plain HTML, CSS and JavaScript. The chime is generated in the browser with the Web Audio API, so there are no audio files. Film details are not affiliated with or sourced live from IMDb or JustWatch, which are linked for convenience only.
