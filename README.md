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

## Note - this is not working yet

The instructions in the tutorial are sketchy in places.

Currently getting an error in the Run step when using #!/bin/sh -l   :

        /bin/sh: illegal option -
        ##[error]Docker run failed with exit code 2

And if I remove the -l the Run step has this error:

        standard_init_linux.go:211: exec user process caused "no such file or directory"
        ##[error]Docker run failed with exit code 1

I just found this tip here <https://forums.docker.com/t/standard-init-linux-go-175-exec-user-process-caused-no-such-file/20025/2>

        I had to run dos2unix on the entrypoint script. Wish the error message was more descriptive.

Looks like crlf on DOS / Linux wasn't appropriate. Giving it a try now.
