# ADO Pipeline Template for Docker Login

This template contains an ado pipeline yaml that can be extended under other pipelines to login to the docker

## use case

You need to have a service connection related to GitHub on the Azure DevOps project.
To call this in your pipeline you can follow this example:

   ```yaml
  # azure-pipeline.yml
  parameters:

    - name: RegistryToken
      type: string

  resources:
    repositories:
      - repository: DockerLogin
        type: github
        name: knoldus/ado.docker.login
        ref: <respective branch name>
        endpoint: '<GitHub Service Connection>'

  steps:

  - template: login.yml@DockerLogin
    parameters:
      dockerRegistryServiceConnection: ${{ parameters.RegistryToken }} 
  ```

You can also use Variable Group and Azure Key Vault for values.
