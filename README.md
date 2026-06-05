# MLibrary fork of Voxpupuli Test Gem

## Why?

As of this writing, [voxpupuli-test](https://rubygems.org/gems/voxpupuli-test) depends on a version of [rubocop](https://rubygems.org/gems/rubocop/) that is incompatible with any release of [standardrb](https://rubygems.org/gems/standardrb/).

We don't use any of voxpupuli-test's rubocop support, but we depend on standardrb.

## Patches

- remove rubocop dependency, so standardrb works
- disable rubycop rake tasks
- add this README

## Make a new release

When upstream cuts a new release:
- If they no longer have a hard conflict w/ standardrb, consider moving back to the upstream gem (keep in mind, this will bring back in some rake tasks we don't use too).
- Sync fork. Pull a local copy.
- Create a new branch that matches the latest tag:
  - `git checkout -b v99.99.99 v99.99.99; git push`
- Fork your new branch:
  - `git checkout -b v99.99.99-patches`
- Re-apply our patches:
  - `git log v14.0.0..v14.0.0-1 --oneline`
  - `git cherry-pick <list of commit sha>`
  - review changes, update as needed (esp. consider any notes to update in this README)
- Push, and open a PR
  - Be certain that the target of the PR is the branch, not master, and definitly not upstream!
- Once CI passes and PR is merged, pull the release branch, tag a release, and push your new tag:
  - `git checkout v99.99.99; git pull`
  - `tag -s v99.99.99-r1 -m v99.99.99-r1`
  - `git push origin tag v99.99.99-r1`

Pushing a tag should automatically create a new release, and upload the gem to GitHub Packages. Note, that at the time of this writing this process is untested.
