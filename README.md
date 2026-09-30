# pubsub.robonomics.network

Status page and list of the Robonomics IPFS pubsub nodes — published with GitHub Pages at
**https://pubsub.robonomics.network**.

- `nodes.json` — the list of active nodes: peer IDs, multiaddrs per transport (wss, QUIC, WebTransport, tcp), topics.
  **This is the only file to edit** when nodes are added, removed or change their IDs.
- `index.html` — static page (no build step, no dependencies). It reads `nodes.json` and checks every node live from
  the visitor's browser via `GET https://N.pubsub.robonomics.network/health` (`200 ok`, or `503 down` when the node's
  IPFS daemon is not operational); refreshes every 30 s.

## Connect

```
/dnsaddr/pubsub.robonomics.network
```
resolves (TXT `_dnsaddr.pubsub.robonomics.network`) to the wss address of every node, e.g.
`ipfs bootstrap add /dnsaddr/pubsub.robonomics.network` or add it to `Peering.Peers` / a js-libp2p bootstrap list.

Topics: `sensors.social/v1`, `sensors.social/v1/staging`, `airalab.lighthouse.5.robonomics.eth`.

## Adding a node

1. Deploy the node (kubo, `/health` endpoint with `Access-Control-Allow-Origin: *`).
2. Add it to `nodes.json`.
3. Add its `dnsaddr=/dns4/N.pubsub.robonomics.network/tcp/443/wss/p2p/<peer ID>` TXT record to `_dnsaddr.pubsub.robonomics.network`.

## Hosting

GitHub Pages from the `master` branch root, custom domain from `CNAME`. DNS: `pubsub.robonomics.network CNAME airalab.github.io`
(Cloudflare: DNS only).

Local preview: `python3 -m http.server 8000` and open http://localhost:8000.
