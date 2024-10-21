
Secret must be set under `Secrets and Variables > Dependabot`, API:

- Fine-grained personal access token basically that's the same that you specify in YAML for `GITHUB_TOKEN`
- Classic Token needs scopes `repo`, `workflow`, `write:packages`

## Clean Testing

For clean testing, re-create the Repository on GitHub when it gets to polluted with Tags and Releases:

    gh repo delete --yes
    gh repo create --public ${${$(git remote get-url origin)##*/}%.git}
    
    gh secret set DEPENDABOT_TOKEN --body '<TOKEN>' --app dependabot
    gh secret set SEMANTIC_RELEASE_TOKEN --body '<TOKEN>'
    gh secret set DOCKERHUB_TOKEN --body '<TOKEN>'

    git tag | xargs git tag -d
    git push -u origin master
