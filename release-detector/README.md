Exemple de job qui va déployer une release automatiqument à 23h.
Il faut ajouter le secret CI_TAG_DEPLOY_KEY sur le repos. créer une deploy key github pour ce secret.

name: "release"

on:
  schedule:
    - cron: "0 23 * * *"

jobs:
  release:
    runs-on: [self-hosted]
    steps:
    - name: release
      uses: gads-citron/actions-collection/release-detector@master
      with:
        ssh-private-key: ${{ secrets.CI_TAG_DEPLOY_KEY }}
        gh-oauth-token: ${{ secrets.CI_GITHUB_OAUTH_TOKEN }}