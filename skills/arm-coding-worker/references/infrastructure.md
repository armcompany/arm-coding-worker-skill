# Infrastructure and delivery changes

Identify the affected environment, module/chart/resource, state boundary, provider/tool versions, and repository validation workflow. Inspect dependencies and consumers of outputs or configuration. Keep application source outside scope unless an actual interface change requires it.

Use relevant syntax/format checks, static validation, rendered manifests, policy checks, and plans/diffs. Commands are candidates until repository definitions confirm them. Planning can access credentials, remote state, providers, or external data sources; determine side effects and authorized environment before execution.

Review autoscaling/resource limits, minimum/maximum capacity, health checks, permissions, networking, availability, costs, state locks, and rollback/recovery only as affected. Inspect the proposed resource changes, including replacements and deletions; a syntactically valid file does not establish operational safety.

Distinguish preparation and validation from application: Terraform apply, cluster mutation, production deployment, DNS changes, secret rotation, and release submission require existing authorization for the exact environment and action. Do not infer that authority from a request to edit configuration.

CI changes need validation of trigger conditions, job dependencies, permissions, secrets use, and relevant commands. Do not loosen a failing gate simply to make the pipeline green. Avoid blindly installing providers or rebuilding every application because a workflow exists.
