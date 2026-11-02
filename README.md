# ASP.NET Core service for Kubernetes on Wodby

Build and run ASP.NET Core applications on Kubernetes with Wodby.

This repository defines the Wodby service manifests and operational
configuration for ASP.NET Core.

- [Browse Wodby services](https://wodby.com/services)
- [Wodby service documentation](https://wodby.com/docs/2.0/services/)
- [Service manifest reference](https://wodby.com/docs/2.0/services/template/)

## Start with a boilerplate

Use one of the boilerplates exposed by this service to start with compatible
build configuration and Wodby CI:

- [ASP.NET Core boilerplate](https://github.com/wodby/aspnetcore-boilerplate)

## Wodby stacks using this service

- [ASP.NET Core application stack](https://github.com/wodby/stack-aspnetcore)

## Service overview

| Property | Manifest configuration |
| --- | --- |
| Service name | `aspnetcore` |
| Type | Application service |
| Inherits from | [`dotnet`](https://github.com/wodby/service-dotnet) with version constraint `^1.0.0` |
| Application build | Git source connection enabled; Dockerfile: `Dockerfile`; boilerplates: ASP.NET Core boilerplate |

## Use this service

Use this service through [ASP.NET Core application stack](https://github.com/wodby/stack-aspnetcore), or reference
`aspnetcore` from a custom Wodby stack.

A service is a reusable component and does not deploy by itself. The stack
defines its links, settings, versions, resources, and relationship to the rest
of the application.

The service inherits the .NET image, versions, build, links and development
workspace from [`dotnet`](https://github.com/wodby/service-dotnet) and sets
`ASPNETCORE_FORWARDEDHEADERS_ENABLED=true`, so ASP.NET Core applies the
forwarded client address and scheme from Wodby's gateway.

## Maintain a custom version

1. Fork this repository.
2. Edit the service manifest and referenced files.
3. Import the repository as a [Git-backed service](https://wodby.com/docs/2.0/services/create/#create-a-git-backed-service).
4. Reference the service from a stack manifest.

Validate the manifests with:

```bash
wodby service validate-manifest service.yml --org <org-id>
```

See the [service manifest reference](https://wodby.com/docs/2.0/services/template/) and the [managed services index](https://github.com/wodby/services).
