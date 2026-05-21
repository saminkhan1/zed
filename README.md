# Zed Single-File Git Diff

This is a Zed editor fork for testing VS Code-style single-file Git diffs in the Git panel.

It lets you select one changed file and open a Project Diff scoped to only that file, so you can review one file at a time instead of accidentally scrolling through every changed file in the project diff.

If you searched for Zed single-file Git diff, Zed Git panel selected-file diff, or viewing one file at a time in Zed's Git changes, this fork is focused on that workflow.

This is an experimental fork for local testing. It is not an official Zed build.

Upstream: [zed-industries/zed](https://github.com/zed-industries/zed)

Base: Zed `v1.3.5` at `0e3bab3c345882d3d500df826c46d2cebe1cb6a8`

## Why

Zed's Git panel shows changed files as separate items, so selecting one file creates a file-scoped expectation: click a file, review that file's diff.

Upstream Zed can show one file's changes if you open the file and expand its inline diff hunks. This fork changes a different workflow: clicking a changed file in the Git panel opens a scoped side-by-side Project Diff for that selected file.

The goal is to reduce review friction when you only want to inspect one changed file and avoid drifting into unrelated diffs while scrolling.

## What Changed

- Selecting a file in the Git panel opens a Project Diff scoped to that file.
- The project-wide diff action still shows all uncommitted changes.
- Switching from the all-files diff back to a selected file narrows the existing diff tab.
- Selected-file diffs load only the selected path instead of scanning and rendering every changed file.
- Selected-file diff scrolling is clamped so it does not end on a mostly blank page.

## Related Context

- [Zed discussion: Git Diff - Full File View](https://github.com/zed-industries/zed/discussions/33773)
- [Reddit: one file at a time in Zed's Git diff](https://www.reddit.com/r/ZedEditor/comments/1n965fz/is_there_a_way_to_view_one_file_at_a_time_in_zeds/)

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

License and upstream project details remain with the original Zed source tree.
