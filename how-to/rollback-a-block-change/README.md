# How To Rollback a Block Change

If you published a minor change (major changes cannot be rolled back) and for some reason you want to roll it back, here is how you can do it.

We will assume that you released a change that was not supposed to reach production yet. Something like this:

```
element release -n "a release"
```

## 1. Checkout Your Repo to the Previous Minor Release Commit

As we recommended in the [how to track block versions document](../track-block-versions), it is a good practice to commit every time
you release a version. The first step is to locate the last commit you released and checkout your repo to use that commit:

```sh
git checkout latest_released_commit
```

## 2. Issue the Rollback Command

Next, you can run the element command to rollback:

```
element rollback
```

At this point, your block users will get the previous released version. The version you rolled back is removed from the server.

If you had multiple minor releases linked to the major release, every `rollback` command will jump back one release until reaching the major.
The major version cannot be rolled back.

## 3. Fix the Error That Generated The Rollback

If you want to fix the issue, just fix it and release again if needed. Remember to commit the new release.

```sh
npm run build
element release -n "release notes"
git commit -am "new release"
```
