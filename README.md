# DemoGitHubActions
Sandbox for GitHub actions

Following the instructions from: <https://help.github.com/en/articles/creating-a-docker-container-action>

This action prints "Hello World" or "Hello" + the name of a person to greet to the log.

## Inputs

### 'who-to-greet'

**Required** The name of the person to greet. Default '"World"'.

## Outputs

### 'time'

The time we greeted you.

## Example usage

uses: JimBlizzard/DemoGitHubActions@v1
with:
    who-to-greet: 'Mona the Octocat'
