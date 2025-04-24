Reproducer for a [Renovate looping bug](TODO).

The following commands assume the following exported environment variables:
```
RENOVATE_PLATFORM=github
RENOVATE_REPOSITORY=<username>/renovate-looping-reproducer

```

To reproduce the bug, fork this repo and then run the following **once**:

```
RENOVATE_CONFIG={"extends":[":pinDevDependencies"]} renovate
```

Renovate creates the PR to pin the dev dependency first and then the tauri-monorepo PR without the npm dependency. This is not the only way to achieve the bug (and not one you are likely to see normally), but it's seemingly reproducible.

Then on the following runs use the same command without the additional config:

```
renovate
```

This closes the dependency pinning PR. Observe how the tauri-monorepo PR alternates between having only npm or only cargo updates.
