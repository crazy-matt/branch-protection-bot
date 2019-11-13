# Branch Protection Bot
A bot tool to temporarily disable and re-enable "Include administrators" option in branch protection

Github doesn't have a way to give a Bot access to override the branch protection, specifically if you [include administrators](https://github.com/isaacs/github/issues/1390).
The only possible solution is to disable the `include administrators` option. This increases risk of accidental pushes to master from administrators (I've done it a few times).
This tool doesn't completely solve the problem of accidents happening but reduces the chances by closing the window.

The intended use of this tool is to is in a CI/CD pipeline where you require temporary access to allow a administrator Bot push to a branch.

## How it works
1. Your automated pipeline is kicked off
1. Before you push to github you run this tool to disable `Include administrators`
1. Push to the repository
1. After you push to github you run this tool to enable `Include administrators`

## Example usage
```
docker run -e ACCESS_TOKEN=abc123 -e BRANCH=master -e REPO=branch-protection-bot -e OWNER=benjefferies benjjefferies/branch-protection-bot
```

## Github repository settings
The Bot account must be in the `Restrict who can push to matching branches` list.