---
title: Customizing your profile
intro: You can customize your profile so that other people can get a better sense of who you are and the work you do.
redirect_from:
  - /articles/customizing-your-profile
  - /github/setting-up-and-managing-your-github-profile/customizing-your-profile
versions:
  fpt: '*'
  ghes: '*'
  ghec: '*'
topics:
  - Profiles
children:
  - /about-your-profile
  - /about-your-organizations-profile
  - /personalizing-your-profile
  - /managing-your-profile-readme
  - /pinning-items-to-your-profile
  - /setting-your-profile-to-private
---

# Based on https://nextjs.org/docs/pages/building-your-application/deploying/ci-build-caching#github-actions

name: Cache Nextjs build cache

description: Cache the .next/cache according to best practices

runs:
  using: 'composite'
  steps:
    - name: Cache .next/cache
      uses: actions/cache@13aacd865c20de90d75de3b17ebe84f7a17d57d2 # v4.0.0
      with:
        path: ${{ github.workspace }}/.next/cache
        # Generate a new cache whenever packages or source files change.
        key: ${{ runner.os }}-nextjs-${{ hashFiles('**/package-lock.json') }}-${{ hashFiles('**/*.ts', '**/*.tsx') }}
        # If source files changed but packages didn't, rebuild from a prior cache.
        restore-keys: |
          ${{ runner.os }}-nextjs-v13
