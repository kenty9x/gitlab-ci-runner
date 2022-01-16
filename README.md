# Run Gitlab CI in own system

- Create a folder somewhere in your system, ex.: C:\GitLab-Runner.
- Download the binary for 64-bit or 32-bit and put it into the folder you created.
- Make sure to restrict the Write permissions on the GitLab Runner directory and executable. 
- Run an elevated command prompt
- Register a runner.
- Install GitLab Runner as a service and start it. You can either run the service using the Built-in System Account (recommended) or using a user account.