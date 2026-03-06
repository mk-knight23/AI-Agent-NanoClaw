# Swarm Collective Specification

NanoClaw is the first agent to support native **Swarm Logic**.

### Active Team Configurations:
- **Research_Swarm**: 3 nodes (Browser, Data, Summarizer).
- **Engineering_Swarm**: 2 nodes (Linter, Coder).
- **Security_Swarm**: 1 node (Audit-Only).

### Isolation Mode:
- Every swarm node runs in a dedicated **Linux Container**.
- Filesystem access is strictly limited to `/workspace`.
