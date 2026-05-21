# Zed Selected-File Git Diff

This fork adds VS Code-style selected-file diffs to Zed's Git panel.

Upstream: [zed-industries/zed](https://github.com/zed-industries/zed)

Base: Zed `v1.3.5` at `0e3bab3c345882d3d500df826c46d2cebe1cb6a8`

## What Changed

- Selecting a file in the Git panel opens a Project Diff scoped to that file.
- The project-wide diff action still shows all uncommitted changes.
- Switching from the all-files diff back to a selected file narrows the existing diff tab.
- Selected-file diffs load only the selected path instead of scanning and rendering every changed file.
- Selected-file diff scrolling is clamped so it does not end on a mostly blank page.

## Files Touched

- `crates/git_ui/src/git_panel.rs`
- `crates/git_ui/src/project_diff.rs`
- `crates/project/src/git_store/branch_diff.rs`

## Verify

```sh
cargo fmt --check
git diff --check
cargo check -p project -p git_ui
cargo test -p git_ui
cargo build -p zed --profile release-fast
```

## Build

```sh
cargo build -p zed --profile release-fast
```

The built binary is:

```text
target/release-fast/zed
```

## Notes

This is an experimental fork for local testing. It is not an official Zed build.

License and upstream project details remain with the original Zed source tree.
