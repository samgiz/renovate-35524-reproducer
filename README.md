Reproducer for a [Renovate looping bug](https://github.com/renovatebot/renovate/discussions/35524).

I assume the following environment variables have been exported with appropriate values:
```
RENOVATE_PLATFORM=github
RENOVATE_REPOSITORY=<username>/renovate-35524-reproducer
RENOVATE_TOKEN=<...>
```

To reproduce the bug, fork this repo and then run the following **once**:

```
RENOAVTE_CONFIG="{\"packageRules\":[{\"matchPackageNames\":[\"@tauri-apps/cli\"],\"allowedVersions\":\"<=2.4.0\"}]}" renovate
```

This will make sure that `@tauri-apps/cli` does not get included in the initial Renovate PR.

Then on the following runs use renovate without the additional config:

```
renovate
```

Observe how the `tauri-monorepo` PR alternates between having only pnpm or only cargo updates.
