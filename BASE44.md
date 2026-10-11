# Base44 integration: dark mode

The Coil & Core app already has full light and dark themes built in. Base44 does
not need to restyle anything. It only needs to tell the embedded app which theme
to use, in one of the ways below.

The app lives at `https://prostrategyprofiler.github.io/coil-and-core/` and is
shown on coilandcore.com inside a full-screen iframe.

## Prompt to paste into Base44's agent

> The page embeds the Coil & Core app in a full-screen iframe. Do not restyle
> or re-implement the app. It has its own light and dark themes and is
> controlled only through the iframe, as follows.
>
> 1. Set the iframe `src` to
>    `https://prostrategyprofiler.github.io/coil-and-core/?theme=auto`
>    so the app follows the visitor's device setting by default.
> 2. If the site has its own light/dark toggle, keep the app in sync by sending
>    a message to the iframe whenever the site theme changes:
>    `iframe.contentWindow.postMessage({ type: "coilcore:set-theme", theme: "dark" }, "*")`
>    with `theme` set to `"dark"`, `"light"` or `"auto"`.
>    Also send it once on the iframe's `load` event so the first view matches.
> 3. If the site has its own toggle, add `&themeSwitch=hide` to the iframe
>    `src` so the app's built-in Auto/Light/Dark switch is hidden and visitors
>    only see one control.
> 4. Make the page around the iframe match: background `#0D151E` in dark mode
>    and `#E9EDF1` in light mode, no padding or border around the iframe, and
>    the iframe 100% wide and 100vh tall.
> 5. Optional: listen for the app's reply to know its current theme:
>    `window.addEventListener("message", e => { if (e.data?.type === "coilcore:theme") { /* e.data.theme is "dark"|"light"|"auto", e.data.resolved is "dark"|"light" */ } })`.

## Reference

| Control | Values | Effect |
|---|---|---|
| `?theme=` on the iframe URL | `dark`, `light`, `auto` | Theme on first load. `auto` follows the device. |
| `?themeSwitch=hide` | `hide` | Hides the app's own Auto/Light/Dark switch. |
| message `{type:"coilcore:set-theme", theme}` | `dark`, `light`, `auto` | Changes the theme live, without reloading. |
| message `{type:"coilcore:get-theme"}` | none | The app answers with `{type:"coilcore:theme", theme, resolved}`. |
| message from the app `{type:"coilcore:theme", theme, resolved}` | | Sent on load and after every change. |

Priority inside the app, highest first: the URL parameter, then a message from
the embedding page, then the visitor's own choice in the app's switch (remembered
in that browser), then the device setting.

Theme colours, in case the surrounding page should match:

| | Light | Dark |
|---|---|---|
| Page background | `#E9EDF1` | `#0D151E` |
| Card surface | `#FFFFFF` | `#15202C` |
| Text | `#141E29` | `#E3EBF3` |
| Accent (copper) | `#A8551F` | `#E2924F` |
