# Murmur Debate v2 — Gemini 3.1 Pro Preview

## Where Gemini 3.1 Pro Pushes Back on Claude

| Critique | Claude | Gemini 3.1 Pro |
|---|---|---|
| Capabilities unsigned | CRITICAL flaw | Agrees — fatal flaw |
| Description re-signing = friction | Footgun | **Disagrees** — it's non-repudiation. Description IS the contract. Re-vouching is correct. |
| LWW loses data | Bad for decentralized | **Half-disagrees** — only keyholder can update, so no real concurrent edits. Real issue is clock drift (fake timestamps). |
| Referrer orphans | Needs cascading | **Disagrees on solution** — cascading deletes = DOS vector. Orphans should become "Degraded" status instead. |
| Key distribution | Critical gap | Agrees — `who` MUST be the pubkey or DID |
| Revocation | No path | Agrees — needs signed tombstones |

## Gemini's Original Proposals for v0.6

1. **Identity = pubkey, names = claims** — `did: ed25519:<pubkey>`, name is just metadata
2. **Voucher Graph > Referrer Tree** — decouple creator from endorsers, any agent can sign endorsements, search ranking by endorsement count
3. **Tombstones + Epochs** — integer nonce prevents resurrection of deleted agents
4. **Reject Markdown** — cryptographic signing requires deterministic serialization, MD parsing is too fragile
5. **Reject global P2P embeddings** — model incompatibility + bandwidth. Instead: gossip text, embed locally

## Key Gemini Quote
> "Murmur is brilliant in its simplicity, but v0.5 is trying to solve P2P trust and identity with web2 document logic."
