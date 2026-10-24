# IdPlatformKit

**A reference Internal Developer Platform, built from open-source building blocks and runnable on your laptop.**

IdPlatformKit shows, end to end, how a platform team can give developers self-service access to secured infrastructure: a team asks for what it needs from a developer portal, and gets an isolated, policy-compliant environment a few minutes later, without opening a ticket.

Everything is designed to be read, run and reused: each design choice is documented, and the whole stack starts locally on [kind](https://kind.sigs.k8s.io/) with no cloud account.

## How it fits together

```mermaid
flowchart LR
    Dev([Developer]) -->|fills a form| Portal[Portal<br/>Backstage]
    Portal -->|opens a PR with a claim| Repo[(Instances repo)]
    Repo -->|synced by| Argo[Argo CD]
    Argo --> XP[Orchestrator<br/>Crossplane v2]
    XP --> NS[Tenant namespace<br/>quota · RBAC · network policy]
    XP --> Bao[OpenBao namespace<br/>isolated secrets]
    XP --> PG[Postgres database]
```

## Repositories

| Repository | Role | Stack |
|---|---|---|
| [**Orchestrator**](https://github.com/idPlatformKit/Orchestrator) | Self-service infrastructure: a library of Crossplane compositions (`Tenant`, `PostgresDatabase`), end-to-end tested on kind | Crossplane v2, OpenBao, provider-sql, kustomize |
| [**portal**](https://github.com/idPlatformKit/portal) | Developer portal: software catalog, GitHub authentication, org and team sync, and the "New Tenant" Software Template | Backstage |
| [**instances**](https://github.com/idPlatformKit/instances) | The claims (`Tenant`, `PostgresDatabase`) that should exist on the platform, validated in CI and synced by Argo CD | YAML, Crossplane CLI |

## Where it stands

- ✅ Multi-tenant namespaces with per-tenant secrets isolation (OpenBao namespaces + Kubernetes auth)
- ✅ Self-service Postgres databases
- ✅ Backstage portal with GitHub sign-in and group import
- ✅ GitOps flow: Argo CD installs the platform and syncs claims from the instances repository
- ✅ Backstage Software Template opening a pull request with a `Tenant` claim, verified end to end: from the form to a provisioned namespace
- ✅ Each tenant's Kubernetes and Crossplane resources visible in the portal
- ✅ Each tenant's OpenBao secrets delivered as Kubernetes Secrets by External Secrets Operator
- ✅ Postgres databases added to a tenant from the portal, linked to it in the catalog, with per-tenant names on the shared server
- 🔜 Kyverno guardrails, a "new app" golden path, per-tenant observability

Detailed roadmap in the [Orchestrator issues](https://github.com/idPlatformKit/Orchestrator/issues?q=label%3Aroadmap).

## Write-ups

- TODO_TITRE_ARTICLE_1 : TODO_LIEN_1
- TODO_TITRE_ARTICLE_2 : TODO_LIEN_2

## Contributing

Issues, questions and ideas are welcome. Issues labelled [`good first issue`](https://github.com/idPlatformKit/Orchestrator/labels/good%20first%20issue) are a good starting point.

---

Built by [Anas Touil](TODO_LIEN_LINKEDIN), Platform Engineer (CKA, CKAD).
