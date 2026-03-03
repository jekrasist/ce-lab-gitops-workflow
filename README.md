# Lab M5.03 - GitOps Workflow Implementation

## GitOps Flow

\`\`\`
develop branch ──push──► Deploy to dev environment
    │
    └──PR──► Promotion Check (plan against prod)
                │
                └──merge──► main branch ──push──► Deploy to prod environment
\`\`\`

## Environments

| Environment | Branch | Versioning | Log Retention | State Key |
|-------------|--------|------------|---------------|-----------|
| dev | develop | Disabled | 7-14 days | m5-03-gitops/dev/terraform.tfstate |
| prod | main | Enabled | 90 days | m5-03-gitops/prod/terraform.tfstate |

## Workflows

| Workflow | Trigger | Purpose |
|----------|---------|---------|
| `deploy.yml` | Push to main or develop | Deploy to the matching environment |
| `promotion.yml` | PR targeting main | Plan prod changes and post to PR |

## How to Promote Changes
1. Make changes on `develop` and push
2. Verify the dev deployment succeeds
3. Open a PR from `develop` to `main`
4. Review the production plan in the PR comment
5. Merge to deploy to production

