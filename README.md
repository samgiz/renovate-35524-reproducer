Reproducer for a [Renovate looping bug](https://github.com/renovatebot/renovate/discussions/35524).

I assume the following enrironment variables have been exported with appropriate values:
```
RENOVATE_PLATFORM=github
RENOVATE_REPOSITORY=<username>/renovate-35524-reproducer
RENOVATE_TOKEN=<...>
```

To reproduce the bug, fork this repo and then run the following **once**:

```
RENOVATE_CONFIG={"extends":[":pinDevDependencies"]} renovate
```

Renovate creates the PR to pin the dev dependency first and then the `tauri-monorepo` PR without the pnpm dependency. This is not the only way to achieve the bug (and not one you are likely to see normally), but it seems to be reproducible behaviour.

Then on the following runs use renovate without the additional config:

```
renovate
```

This will close the dependency pinning PR and group all the dependencies in the `tauri-monorepo` PR. Observe how the `tauri-monorepo` PR alternates between having only pnpm or only cargo updates.
