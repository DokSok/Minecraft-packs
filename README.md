# minecraft-packs

Modpacks for doksok.com Minecraft events, one folder per event, defined with
[packwiz](https://github.com/packwiz/packwiz). Decided in ADR 0042 (DokSok/sinistercyb).

How a pack reaches people:

1. The event's Pelican server runs `packwiz-installer -g -s server <raw URL of pack.toml>` before it starts,
   so the server always matches the pack.
2. AutoModpack (in every pack, `side = "both"`) serves the pack from the game server to players, who sync
   before joining. Server-only mods stay off players' machines.

## Rules

- **No jars, no secrets.** Packs hold versions, download URLs, hashes and default settings only. No server
  addresses, player data or tokens: this repo is public.
- **Mark each mod's side:** `client`, `server` or `both`. The server's own mods (FabricExporter, Spark) are
  `server`; the players' set is `client`.
- **Settings are first-launch defaults.** Files under `config/` and `options.txt` are delivered once and
  players may change them (AutoModpack 4.x `allowEditsInFiles`, the default). To enforce one for an event,
  remove its path from `allowEditsInFiles` in that server's AutoModpack config. In 4.x, settings files reach
  players only if they're also listed in `syncedFiles`.
- **Pin AutoModpack** to a stable release (`packwiz pin automodpack`); `packwiz update --all` would otherwise
  pick release candidates.
- Every change goes through a PR.

## Working on a pack

```sh
nix run nixpkgs#packwiz -- modrinth add <mod>   # in the event folder
nix run nixpkgs#packwiz -- refresh              # after editing files by hand
nix run nixpkgs#packwiz -- serve                # try it locally
```

## Packs

| Folder | Event | Minecraft | Fabric |
|---|---|---|---|
| `cube-drop-test/` | Cube Drop Test server | 26.2 | 0.19.3 |
