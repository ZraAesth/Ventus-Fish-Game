Ventus's Fish Pond — final controls update

This builds on the approved sound/Home Screen version. Fish artwork,
background, sound synthesis, touch handling, spawn settings, steering,
turn timing, tail animation and normal swimming are preserved.

CONTROLS
- More Fish: starts at 3. Each press adds one fish using the same spawn
  function, without resetting existing fish or score. Maximum 10; the
  button becomes disabled at the cap. Catching replaces one fish and
  keeps the selected population.
- Turbo ON/OFF: defaults OFF. ON multiplies travel speed by 1.5, or 1.85
  during existing darts. Steering, random turn/dart timing, wave motion
  and tail artwork are unchanged. OFF restores original travel speed.
- Sound ON/OFF: keeps the existing quiet, 160 ms catch bloop. Misses are
  silent. The existing gesture-based iOS Web Audio setup is unchanged.
- Hide: hides the entire bar and hint. A small Menu button appears in the
  top-right corner; tap it to restore the bar. Fish keep swimming, and
  catching, sound, score and settings keep working while the bar is hidden.

The bar buttons are at least 44 pixels high and 60 pixels wide. The restore
button is 44 by 44 pixels. The bar fits both iPad portrait and landscape.

DEPLOYMENT AND HOME SCREEN
Manually upload ZIP contents with index.html at the site root. Keep _headers
beside it on Netlify for the existing external-script-blocking CSP. The HTML
also retains its early meta CSP. Nothing was automatically deployed.

On the iPad, open the hosted website in Safari, choose Share > Add to Home
Screen > Add, then launch its icon for standalone play without Safari's
address/search bar and browser navigation controls. If an older icon does
not pick up updated metadata, remove it and add it again.

TESTING
66 checks passed using Acorn ES5 parsing and Playwright with Chromium
154.0.8037.57 on Linux. Tests exercised actual touch input on each control,
adding 3 through 10 fish, the cap, original-fish preservation, independent
Turbo/sound/population settings, catching with the bar hidden, corner
restore, 44-pixel targets in both orientations, and ten-fish animation.

A seeded comparison matched every fish state against the previous normal
movement for 5,000 updates with Turbo OFF. Turbo travel multipliers were
checked separately while steering, timing and speed state remained equal.
Source comparisons confirmed that fish drawing, background, rendering,
spawning, audio and touch functions are byte-for-byte unchanged.

Regression checks covered catching and replacement, actual Web Audio graph
output, 160 ms duration, low volume, muting, gesture initialization, prefixed
webkitAudioContext, suspended audio resume, silent play if audio fails,
canvas sizing, and CSP blocking of a simulated external Netlify HUD script.

The HTML remains self-contained, dependency-free at runtime and ES5. The
ZIP has no test hooks, frameworks, external assets or audio downloads.

Real iPad 2 / Safari 9 performance, audio and Home Screen launch remain
untested. No actual Netlify deployment was tested. The existing CSP blocks
external scripts but permits inline scripts; optional host HUD injection
should be disabled if it inserts incompatible inline code.
