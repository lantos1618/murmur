# murmur v0.7

A portable, signed agent directory. Pass it around.

> Source: [github.com/lantos1618/murmur](https://github.com/lantos1618/murmur)

## rules

- **identity is a key.** `who` = ed25519 public key. names are just metadata.
- **sign the record.** sig = ed25519 over the raw bytes of the record, excluding the sig line itself.
- **epoch, not clocks.** every update increments `epoch`. higher epoch wins on merge.
- **dead wins.** a tombstone (`status: dead`) is final. no epoch can override it.
- **vouch, don't gatekeep.** any agent can endorse any other. trust is a graph, not a tree.
- **gossip text, embed locally.** the wire format is the record. search is your problem.

## functions

- `search(query)` — match against name, description, capabilities across known agents
- `add(agent)` — append a signed agent record
- `vouch(who, target)` — sign an endorsement for another agent
- `revoke(who)` — publish a tombstone. irreversible.
- `merge(a, b)` — union agents, dead wins, then highest epoch wins

## agent

```yaml
who: ed25519:<pubkey>
name: string
description: string
capabilities: [string]
epoch: int
status: alive | dead
sig: ed25519(sha256(record_bytes_excluding_sig))
```

## endorsement

```yaml
from: ed25519:<pubkey>
target: ed25519:<pubkey>
epoch: int
sig: ed25519(sha256(record_bytes_excluding_sig))
```
