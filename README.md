# Run Gitlab CI in own system

- Create a folder somewhere in your system, ex.: C:\GitLab-Runner.
- Download the binary for 64-bit or 32-bit and put it into the folder you created.
- Make sure to restrict the Write permissions on the GitLab Runner directory and executable. 
- Run an elevated command prompt
- Register a runner.
- Install GitLab Runner as a service and start it. You can either run the service using the Built-in System Account (recommended) or using a user account.

# Gitlab CI runner in windows OS using Docker

- Create an empty directory somewhere on your machine to store the runner config file in (e.g. C:\gitlab-runner\config). This will persist even when the container shuts down.
- Check docker is running correctly
docker version
- Create the docker container
docker run -d --name gitlab-runner --restart always -v C:\gitlab-runner\config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock gitlab/gitlab-runner:latest
- Check container is running
docker container list
- Register the docker container with GitLab. Replace the <URL> and <TOKEN> in the command below with the values found in GitLab under your project settings -> CI/CD ->Runners -> Setup a specific runner manually.
docker run --rm -t -i -v C:\gitlab-runner\config:/etc/gitlab-runner gitlab/gitlab-runner register --non-interactive --executor "docker" --docker-image alpine:latest --url "<URL>" --registration-token "<TOKEN>" --description "docker-runner" --run-untagged="true" --locked="false"
- In GitLab under the runners section you should see the runner listed:
- Kick off the CI/CD pipeline and the runner should handle the build!