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

## Note - this is not working yet (fixed it below)

The instructions in the tutorial are sketchy in places.

Currently getting an error in the Run step when using #!/bin/sh -l   :

        /bin/sh: illegal option -
        ##[error]Docker run failed with exit code 2

And if I remove the -l the Run step has this error:

        standard_init_linux.go:211: exec user process caused "no such file or directory"
        ##[error]Docker run failed with exit code 1

## Potential fix

I just found this tip here <https://forums.docker.com/t/standard-init-linux-go-175-exec-user-process-caused-no-such-file/20025/2>

        I had to run dos2unix on the entrypoint script. Wish the error message was more descriptive.

Looks like crlf on DOS / Unix wasn't appropriate. Giving it a try now.

## Yes, that was the fix for the entrypoint.sh file. Had to run dos2unix

## "Challenges" with the tutorial

- The instructions did not mention creating a git tag. Obvious now, but took a few minutes to figure out why the action wasn't being run at all.
- The instructions say to "make sure to make you *entrypoint.sh* file executable," but it doesn't say where to do that. The CHMOD command needs to be added to the Dockerfile between the COPY and ENTRYPOINT lines.
- It was confusing the way the instructions described how to use a private action. The *Hello world action step* in *main.yml* in the example should have something like *{yourGitHubAccountName}/hello-world-docker-action@v1*. I spent a while going in circles with that.
- Be sure if you're using WSL to run *dos2unix* on the entrypoint.sh file. Otherwise you'll run into some interesting problems noted above.
