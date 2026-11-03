# ASP.NET Core on Wodby

This service is the .NET service with settings for ASP.NET Core applications. Everything in the .NET service's guidance applies: the build, port 8080, linked-service variables, Data Protection keys and the development workspace.

## What this service adds

- `ASPNETCORE_FORWARDEDHEADERS_ENABLED` is `true`. ASP.NET Core then applies the `X-Forwarded-For` and `X-Forwarded-Proto` headers that Wodby's gateway sets, so `HttpContext.Request.Scheme` is `https` for visitors on HTTPS, generated links and redirects use it, and `Connection.RemoteIpAddress` is the visitor's address. Do not add `UseForwardedHeaders` with other settings, and do not add `UseHttpsRedirection`: TLS ends at the gateway, and checks inside the environment use plain HTTP.
- The ASP.NET Core boilerplate, which restricts host names to `WODBY_HOSTS`, the app service's name and `localhost`, and answers `/healthz`.

## Environment

- `ASPNETCORE_ENVIRONMENT` is not set; ASP.NET Core falls back to `DOTNET_ENVIRONMENT`, which is `Development` in development environments. Elsewhere the application runs as `Production`, so `appsettings.Production.json` applies and the developer exception page is off.
- Configuration from environment variables uses `__` for nesting: a variable on the service named `ConnectionStrings__Default` is `GetConnectionString("Default")`.

## Check the result

- `curl -s -H "Host: $WODBY_APP_SERVICE_NAME" localhost:8080/healthz` in the container answers `Healthy` when the application uses the boilerplate's health check.
- A `400 Bad Request` with an empty body for a domain usually means host filtering does not allow it: compare the domain with `WODBY_HOSTS` and `AllowedHosts`.
