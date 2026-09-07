# elk-kibana-app

Zerops recipe that installs upstream Kibana (`kibana=8.17.4`) via apt and connects to a sibling Elasticsearch service for the ELK visualization UI.

## Zerops service facts

- HTTP ports: `5601` (`httpSupport: true`)
- Siblings: `elkstorage` (Elasticsearch) — env: `ELASTICSEARCH_URL`, `ELASTICSEARCH_PASSWORD`
- Runtime base: `ubuntu@24.04`

## Zerops

No dev iteration loop — the app is an upstream Elastic binary installed via apt in `prepareCommands`. Changes in this repo only affect the `kibana/` config directory and `zerops.yaml` install pins. Each change requires a full build+deploy through the **Zerops development workflow via `zcp` MCP tools**.

## Notes

- Kibana version pinned to `kibana=8.17.4` in `prepareCommands`; bump the pin to upgrade.
- `PUBLIC_BASE_URL_OVERRIDE` overrides the default Zerops subdomain for `server.publicBaseUrl`; set after configuring a custom domain.
- If Kibana OOMs, raise `NODE_OPTIONS_MAX_OLD_SPACE_SIZE_OVERRIDE` above the default `1024` and redeploy.
