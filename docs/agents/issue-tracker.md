# Issue tracker: GitHub

Issues and specs live in GitHub Issues. Use the `gh` CLI.
Infer the repository from `git remote -v`; `gh` does this automatically inside the clone.

## Conventions

- Create: `gh issue create --title "..." --body-file -`, supplying a heredoc for multiline bodies.
- Read: `gh issue view <number> --json number,title,body,labels,comments`.
- List: `gh issue list --state open --json number,title,body,labels,comments`, adding label or state filters as needed.
- Comment: `gh issue comment <number> --body "..."`.
- Add or remove labels: `gh issue edit <number> --add-label "..."` or `--remove-label "..."`.
- Close: `gh issue close <number> --comment "..."`.

When a skill says "publish to the issue tracker", create a GitHub issue.
When it says "fetch the relevant ticket", read the issue including comments and labels.

## Pull requests as a triage surface

**PRs as a request surface: no.**

If enabled later, use `gh pr` equivalents for reading, commenting,
labelling and closing. Read changes with `gh pr diff <number>`.
Include external authors with authorAssociation CONTRIBUTOR,
FIRST_TIME_CONTRIBUTOR or NONE; exclude OWNER, MEMBER and COLLABORATOR.

Issues and PRs share a number space. For an ambiguous reference,
try `gh pr view <number>`, then fall back to `gh issue view <number>`.

## Wayfinding operations

- Map: one issue labelled `wayfinder:map`, holding Notes, Decisions-so-far and Fog.
- Children: link tickets as GitHub sub-issues using `gh api`. If unavailable,
  use a task list in the map and `Part of #<map>` in each child.
  Label children `wayfinder:<type>`: research, prototype, grilling or task.
- Blocking: use native GitHub issue dependencies.
  Add an edge with
  `gh api --method POST repos/<owner>/<repo>/issues/<child>/dependencies/blocked_by -F issue_id=<blocker-db-id>`.
  Obtain the database ID with
  `gh api repos/<owner>/<repo>/issues/<blocker> --jq .id`;
  it is not the issue number or node ID.
  If dependencies are unavailable, use `Blocked by: #<n>, #<n>` in the child body.
- Frontier: inspect the map's open children in map order. Skip assigned tickets
  and tickets with open blockers. Native
  `issue_dependencies_summary.blocked_by > 0` means blocked;
  for fallback links, check each blocker's state.
- Claim: `gh issue edit <number> --add-assignee @me` as the session's first write.
- Resolve: comment with the answer, close the ticket, then append a summary
  and link to the map's Decisions-so-far.
