# Reponomics Homebrew tap

Homebrew formulae maintained by [Reponomics](https://github.com/reponomics).

## Install Treestamp

[Treestamp](https://github.com/reponomics/treestamp) creates and maintains directory trees for project documentation, with a command-line interface and a terminal editor.

```sh
brew install reponomics/tap/treestamp
```

Homebrew installs Python, Git, and the application's Python dependencies. Run `treestamp` inside a Git repository to open the editor, or use `treestamp --print` to print a tree. See the [Treestamp documentation](https://github.com/reponomics/treestamp#readme) for editing, checking, and updating documents.

This formula installs from the checksummed PyPI source release. Prebuilt bottles and automatic formula updates are not enabled. Source installations are tested by CI on macOS 26 and Ubuntu 24.04.

To update:

```sh
brew update
brew upgrade reponomics/tap/treestamp
```

## Maintain the formula

Start an update branch from current `main`. Update the PyPI source URL and SHA-256 in `Formula/treestamp.rb` for the exact published release, then resolve its dependencies:

```sh
brew trust --formula reponomics/tap/treestamp
brew update-python-resources --install-dependencies reponomics/tap/treestamp
```

For a newly published main package rejected by Homebrew's release cooldown, review the release and rerun with `--ignore-main-package-cooldown`; this retains the cooldown for dependencies. Review all generated resource URLs, versions, and checksums. The published dependency ranges are resolved for the formula's Python version independently of Treestamp's development lockfile.

Validate the change before submitting a pull request:

```sh
brew style reponomics/tap/treestamp
brew reinstall --build-from-source reponomics/tap/treestamp
brew test reponomics/tap/treestamp
brew audit --strict --online reponomics/tap/treestamp
brew livecheck reponomics/tap/treestamp
```

Use `brew install --build-from-source` for a first installation. Also open the installed terminal editor and verify basic editing. CI checks source installation and the functional formula test on both supported runners. Merge after the PR has been reviewed and both checks pass. Increment the formula's `revision` when repackaging dependency fixes without changing the Treestamp version.

GitHub Actions dependencies are pinned to full commit SHAs; Dependabot proposes updates. Workflow permissions are read-only. Bottle publication and cross-repository release automation require a separate reviewed change.
