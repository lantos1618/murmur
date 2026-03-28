# Murmur v0.5 — Design Debate (Claude vs Gemini)

## Claude's Critique

1. **Capabilities not signed** — can be tampered during merges
2. **Description changes require re-signing** — intentional friction or footgun?
3. **LWW merge loses data** — concurrent edits silently dropped
4. **Referrer removal cascading undefined** — orphaned referees?
5. **No key distribution** — how to verify sigs without public keys?
6. **No revocation** beyond deletion — compromised keys can't be invalidated

## Gemini's Response

### Agreed (with severity ratings):
1. **Capabilities not signed** — CRITICAL. Attacker can alter advertised functionality without invalidating signature
2. **Description re-signing** — Agreed, but nuanced. If description is static attestation, correct behavior. If dynamic, unnecessary friction. Strange asymmetry with unsigned capabilities.
3. **LWW merge** — STRONGLY AGREE. Guarantees silent data loss in decentralized system. HIGH severity.
4. **Referrer cascading** — AGREE. Breaks web-of-trust if foundational node disappears. HIGH severity.
5. **No key distribution** — CRITICAL. Makes signature field "decorative" without ability to verify.
6. **No revocation** — AGREE. Deleting from one file doesn't prevent compromised key reuse elsewhere. HIGH severity.

### Gemini's Additional Critiques:
7. **`who` field ambiguity** — Must be directly linkable to public key. Name? UUID? Key hash?
8. **Signature scope too narrow** — `updated` timestamp not signed either. Attacker can fake timestamps to win LWW merges.
9. **Vague trust propagation** — No trust scores, decay, or hop limits defined
10. **Decentralization model under-specified** — How do files sync? Single global registry or many independent ones?
