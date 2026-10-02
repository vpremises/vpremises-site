# vPremises site content

## Site content

- Audience: global. English is served at `/`; Japanese is served at `/ja/`.
- Publication boundary: local-observation specifications and safe guidance only; no filesystem change, external transmission, or daemon activation.

## Local verification

```bash
pnpm install --offline --frozen-lockfile
pnpm validate:content
pnpm typecheck
pnpm test
pnpm build
```

Run `pnpm dev` only as a foreground loopback preview and stop it with Ctrl+C.
