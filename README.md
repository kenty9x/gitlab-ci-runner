# Run Gitlab runner in Windows system

- Create an empty directory somewhere on your machine to store the runner config file in (e.g. C:\gitlab-runner\config). This will persist even when the container shuts down.
- Check docker is running correctly
docker version
- Create the docker container
docker run -d --name gitlab-runner --restart always -v C:\gitlab-runner\config:/etc/gitlab-runner -v /var/run/docker.sock:/var/run/docker.sock gitlab/gitlab-runner:latest
- Check container is running
docker container list
- docker run --rm -t -i -v C:\gitlab-runner\config:/etc/gitlab-runner gitlab/gitlab-runner register --non-interactive --executor "docker" --docker-image alpine:latest --url "<URL>" --registration-token "<TOKEN>" --description "docker-runner" --run-untagged="true" --locked="false"
- In GitLab under the runners section you should see the runner listed
- Kick off the CI/CD pipeline and the runner should handle the build!