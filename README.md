# Terminal Rain, synced with the real weather

> *"Imagine it synced with real weather"* said a comment under the original reddit post. Well, here it is.

![All weather states](weather-states.gif)

A tiny live weather panel for your terminal, built on top of [rmaake1's terminal-rain-lightning](https://github.com/rmaake1/terminal-rain-lightning). It polls [wttr.in](https://wttr.in) (no API key needed) every 10 minutes and the sky follows the actual forecast where you are:

| Real weather | What you see |
|---|---|
| Clear / sunny | A sun with pulsing rays |
| Cloudy / overcast | Clouds drifting across the screen with parallax, light drizzle |
| Fog / mist | Rolling banks of `░▒` shifting at different speeds |
| Rain | The classic rain, intensity matching the forecast |
| Thunderstorm | Heavy rain and the lightning turns on by itself |

On top of the scene, the current temperature is drawn in a chunky block font, colored by the weather (yellow sun, cyan rain, magenta storm), with the location, condition and a "feels like · humidity · wind" line under it.

## Install

```bash
pipx install git+https://github.com/TVTvirus/terminal-rain-lightning.git
```

Requirements: Python 3.6+, a terminal with `curses` and color support (kitty, Alacritty, etc.). Optional: `ffplay` from FFmpeg for rain/thunder sounds.

## Usage

```bash
terminal-rain
```

That's it. Your location is auto-detected by IP. To pin one:

```bash
terminal-rain --location "Esparza,Puntarenas,Costa Rica" --lang es
```

### Options

*   `--location PLACE`: Location for the real weather (any wttr.in query). Default: auto-detect by IP.
*   `--lang CODE`: Language for the condition text (wttr.in lang code). Default: `en`.
*   `--rain-color COLOR` / `--lightning-color COLOR`: `black`, `red`, `green`, `yellow`, `blue`, `magenta`, `cyan`, `white`. Defaults: `cyan` / `yellow`.
*   `--speed {fast,medium,slow}`: Starting animation speed. Default: `fast`.
*   `--sound` / `--volume {quiet,normal,loud}`: Rain and thunder sounds (needs `ffplay`).
*   `--no-temp`: Turn the weather sync off, original decorative rain (see below).

### Keys

*   `s`: cycle animation speed · `m`: toggle sound · `v`: cycle volume · `q` / `Esc` / `Ctrl+C`: quit.
*   `t` (thunderstorm toggle) only works in `--no-temp` mode: with the sync on, the *real* weather decides when there's a storm. That's the whole point.

### Preview any state (no network needed)

```bash
OJO_CLIMA_TEMP=25 OJO_CLIMA_COND=thunderstorm terminal-rain
```

Conditions can be in English or Spanish (`sunny`, `cloudy`, `fog`, `rain`, `thunderstorm`, ...). The env names come from my terminal dashboard, where this panel lives.

## Just want the original rain?

`terminal-rain --no-temp` gives you the original animation untouched: pure decorative rain, no network, no temperature, and the `t` key toggles thunderstorm mode manually.

![Calm Rain](calmrain.gif)
![Thunderstorm](thunderstorm.gif)

Or install the upstream project directly: [rmaake1/terminal-rain-lightning](https://github.com/rmaake1/terminal-rain-lightning).

## Troubleshooting

*   **Garbled output / colors off**: use a modern terminal with 256-color support and `TERM=xterm-256color` (kitty and Alacritty work great).
*   **No temperature, only rain**: wttr.in unreachable or rate-limited; the panel keeps animating and retries every 10 minutes.
*   **No sound**: install FFmpeg so `ffplay` is on your PATH, then `--sound` or press `m`.

## Credit and license

All the rain and lightning magic is [rmaake1](https://github.com/rmaake1)'s work: this fork just taught it to look out the window. MIT License, same as upstream. See the LICENSE file.
