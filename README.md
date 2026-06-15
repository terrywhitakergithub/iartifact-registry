# iartifact-registry
Public ledger of sealed iArtifact certificates — immutable provenance records for NFT art and digital works.

A public ledger of sealed iArtifact certificates.

Each line is a sealed artifact registered by the iArtifact desktop app:
iA-ID, type, creator, sealed_at, seal_hash

Verify any entry at: [your verifier URL]

Records are append-only. Once an iA-ID appears here it cannot be altered
without changing the commit history — which GitHub timestamps and signs.
