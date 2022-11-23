# get-version.sh

## What is this?

A simple wrapper to `git describe` that shows the version in a nicer way.

## How does the version look like?

* If your git HEAD is tagged, then the version will be exactly the name of your
  tag.
* If your git HEAD is ahead of an existing git tag, it will show the version in
  format `<tag_name>+<number_of_commits>_g<commit_hash>` (e.g. `1.0+1_gcb5eba6`
  is a version of this repo at revision `cb5eba6` that was ahead of tag `1.0` by
  one commit).
* If your git repository doesn't have any tags, `(none)` is used as a git tag.
* If you have uncommitted changes, `_dirty` will be appended to the given
  version.

## Why does it store the version in `.version` file?

Initially I wrote this script for a repository that has `make dist` target. This
means that a tarball of the sources was created with no metadata about git
repository. Therefore, `get-version.sh` failed as it needed `.git` to exist.
In order to fix this, I decided to cache the version in the separate file.
However, `get-version.sh` will first try to populate git data and only use
`.version` as a fallback. Keep in mind also that you need to add this file to
`.gitignore` in order to not get `_dirty` version.