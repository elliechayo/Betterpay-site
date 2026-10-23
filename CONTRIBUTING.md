# Betterpay development workflow

## Branches and review
- Keep main as the stable, reviewed baseline.
- Create a short-lived branch from current main for each change: feat/<name>, fix/<name>, or chore/<name>.
- Open a pull request into main. Use a draft while work is incomplete.
- Review Files changed, check for credentials and private data, and record validation in the PR.
- With one maintainer, self-review and merge the PR; no approving review is required.
- Prefer Squash and merge, then delete the completed branch.
- Use a new PR to revert a problematic change. Do not force-push main.
- A permanent develop branch is unnecessary. Introduce staging/preview environments when the website foundation is chosen.

## Main protection: owner setup required
These are intended settings, not a claim that protection is active.

Open Settings > Rules > Rulesets > New ruleset > New branch ruleset.
Name: Protect main. Enforcement: Active. Bypass list: empty.
Target branches: Include by pattern > main.

Enable:
- Restrict deletions
- Block force pushes
- Require a pull request before merging
  - Required approvals: 0
  - Require conversation resolution before merging

Leave required status checks, required deployments, required code-owner reviews, approval of the most recent push, and signed commits disabled for now.
Do not enable Restrict updates; it can prevent normal PR merges without a bypass actor.
Save, then reopen the ruleset to confirm it is Active and targets main.
An administrator can still edit or disable the ruleset; this is not protection against a compromised administrator account.

Optional repository Settings > General > Pull Requests:
- Enable squash merging.
- Automatically delete head branches.
- Keep auto-merge off until reliable checks exist.

Once real build/lint/test checks run successfully on pull requests, require the exact checks in this ruleset. Do not require nonexistent checks.
When a second regular reviewer joins, consider requiring one approval and dismissing stale approvals.

## Validation before merge
Documentation-only changes: inspect rendered Markdown and links; application tests are not applicable.
Website changes: record the relevant build/lint/test results, preview link, mobile checks, accessibility checks, and rollback approach.
If a check cannot run, explain why and the remaining risk. Do not claim it passed.

## Deployment boundary
A merge is a repository change, not permission to publish.
Keep the existing Wix site, its domains, DNS, and deployment configuration untouched unless explicitly authorized.
Do not add automatic production deployment as part of repository setup.
Keep the repository public unless a visibility change is explicitly approved.
Never commit credentials, environment secrets, merchant/customer information, or private business records.

## One-time verification after enabling rules
- Reopen Settings > Rules > Rulesets and confirm Protect main is Active with no bypass actors.
- Confirm the rule targets main and includes deletion, force-push, and PR restrictions.
- Use a harmless documentation PR to confirm a sole maintainer can merge with zero approvals.
- Verify that main is shown as protected.
Do not test deletion or force pushes against main.
