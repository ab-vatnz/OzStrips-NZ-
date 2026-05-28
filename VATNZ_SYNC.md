# VATNZ OzStrips Sync Workflow

This fork has two long-lived branches:

- `master` is for upstream-safe work and PRs back to `maxrumsey/OzStrips`.
- `vatnz/main` is the VATNZ vaSys release branch. Keep NZ-specific layouts, autofill, settings, and local fixes here.

## Updating From Upstream

Use the GitHub workflow **Sync upstream OzStrips**.

It fetches `maxrumsey/OzStrips`, merges upstream `master` into `vatnz/main`, and opens a PR from:

```text
sync/upstream-ozstrips -> vatnz/main
```

Merge that PR only after checking:

- NZ strip layout files still look right.
- NZ autofill files are still present.
- `AerodromeSettings.xml` still has the intended VATNZ options.
- Any upstream server/DTO/API changes still build.
- The PR build passes.

If the workflow reports a merge conflict, resolve it locally:

```powershell
git checkout vatnz/main
git fetch upstream
git merge upstream/master
```

Fix conflicts, build, commit, and push `vatnz/main`.

## Flow Into EuroScope

After `vatnz/main` is updated, run the EuroScope repo workflow **Sync VATNZ OzStrips vendor**.

That updates `Ozstrips-euroscope/vendor/OzStrips` from this branch and opens a PR there. It does not blindly overwrite EuroScope-adapted files under `src/OzStripsEuroScope.OzStripsGui`; port those changes manually when needed.
