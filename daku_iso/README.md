# DakuOS ISO images

This directory is the destination for built ISO images.

## Naming convention

```
daku-<version>-amd64.iso
```

Example:
```
daku-0.1.0-amd64.iso
```

The version number comes from the `VERSION` file in the repository root.

## Important

- ISO files are **not** committed to Git (they are large binary artifacts).
- Every successful GitHub Actions build produces an ISO with the name above and uploads it as a workflow artifact.
- Download finished ISOs from the **Actions** tab of this repository.
