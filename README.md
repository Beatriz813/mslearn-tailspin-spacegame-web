
# Anotações

## Declação de variáveis
- Declarar a seção 'variables':

```yaml
variables:
  buildConfiguration: 'Release'
  wwwrootDir: 'Tailspin.SpaceGame.Web/wwwroot'
  dotnetSdkVersion: '6.x'
```

- Referenciar a variável entre '$()'

```yaml
steps:
- task: UseDotNet@2
  displayName: 'Use .NET SDK $(dotnetSdkVersion)'
  inputs:
    packageType: sdk
    version: '$(dotnetSdkVersion)'
```

## Templates

Templates funcionam como um módulo que separamos do arquivo de pipeline e utilizamos parâmetros para que sejam reutilizados.

### Parâmetros

- Declarar parâmetros:
```yaml
parameters:
  buildConfiguration: 'Release'
```
- Referenciar o parâmetro entre '${{}}'

```yaml
steps:
- task: DotNetCoreCLI@2
  displayName: 'Build the project - ${{ parameters.buildConfiguration }}'
  inputs:
    command: 'build'
    arguments: '--no-restore --configuration ${{ parameters.buildConfiguration }}'
    projects: '**/*.csproj'
```