# MLibrary fork of Voxpupuli Test Gem

## Why?

As of this writing, [voxpupuli-test](https://rubygems.org/gems/voxpupuli-test) depends on a version of [rubocop](https://rubygems.org/gems/rubocop/) that is incompatible with any release of [standardrb](https://rubygems.org/gems/standardrb/).

We don't use any of voxpupuli-test's rubocop support, but we depend on standardrb.

## Patches

- remove minimum version in rubocop dependency, so standardrb works
- disable rubycop rake tasks
- github actions changes for testing and release
- add this README

## Make a new release

When upstream cuts a new release:
- If they no longer have a hard conflict w/ standardrb, consider moving back to the upstream gem.
- Sync fork. Pull a local copy.
- Create a new branch that matches the latest tag:
  - `git checkout -b release/v99.99.99 v99.99.99`
- List changes between last upstream release tag, and our version:
  - `git log v14.0.0..v14.0.0-4 --oneline`
- Re-apply our patches:
  - `git cherry-pick <list of commit hashes>`
  - review changes, update as needed (esp. consider any notes to update in this README)
- `git push`
- Once CI passes, tag a release, and push your new tag:
  - `git tag -s v99.99.99-1 -m v99.99.99-1`
  - `git push origin tag v99.99.99-1`

Pushing a tag will automatically create a new release. There won't be a gem published, but you can pin to the git tag in your Gemfile.
