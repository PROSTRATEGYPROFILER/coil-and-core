# Coil & Core

A single-file study app for the electrical apprenticeship: flashcards, quizzes,
a 3D lab, the machine shop, ladder-logic trainer and lab, circuit wiring game
and solver, breadboard simulator, Learn courses and a reference tab. Covers
magnetism, AC circuits, DC generators (including Worksheet 19(h)), PLC basics
and motor control centres.

## Hosting

`index.html` at the root of this repository is the whole app. There is no build step and no server: upload the
file to any static host (Base44, Netlify, GitHub Pages, Cloudflare Pages).
The 3D Lab loads Three.js from a public CDN, so the host needs outbound
internet. The Study Focus generator only works inside the claude.ai artifact;
on other hosts it shows a "tutor not available" note and everything else runs.

## Rules of use

The app opens with an acknowledgement that it is a study tool and must never
be used during a test, exam or other assessment. The same notice sits in the
page footer.

## Where it lives

- Official site: https://coilandcore.com (Base44, embedding the GitHub Pages build)
- GitHub Pages build: https://prostrategyprofiler.github.io/coil-and-core/ (redeploys on every push to `main`)
- Private alpha with the Study Focus tutor: https://claude.ai/artifact/MZDjkwg1q2XarhX4iTS1Mp
