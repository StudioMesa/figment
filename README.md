# Figment

Styles for the Figment Squarespace template (Studio Mesa). `styles.less` is the source; a GitHub Action compiles it to `styles.css` on every push to `main`.

## Status: PRIVATE, not served

This repo is private on purpose. The `templates` Cloudflare Worker proxies `raw.githubusercontent.com`, which does not serve private repos, so nothing here reaches any site until the repo is flipped to public. The demo site's header injection has not been pasted yet either.

## Go-live steps (in this order)

1. Paste the finished LESS into `styles.less` and push. Wait for the Action to commit `styles.css`.
2. Flip the repo to **public** (Settings → Danger zone → Change visibility).
3. Verify the Worker serves it:

    ```
    curl -sI "https://templates.studiomesa.workers.dev/main/styles.css?template=figment"
    ```

   Expect `200` and `content-type: text/css`.
4. Paste into the demo site's Header Code Injection:

    ```html
    <link rel="stylesheet" href="https://templates.studiomesa.workers.dev/main/styles.css?template=figment">
    ```

5. Only then duplicate the demo for inventory. Every duplicate carries that URL.

## Blast radius

There is no staging and the Worker caches for 300 seconds. Once public, every push to `styles.less` reaches every Figment site within five minutes. Treat `main` as production from step 2 onward. See `workers/css-delivery/README.md` in the main repo.
