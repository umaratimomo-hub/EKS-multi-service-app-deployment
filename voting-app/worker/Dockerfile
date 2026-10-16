FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /src
COPY Worker.csproj ./
RUN dotnet restore
COPY . .
RUN dotnet publish -c Release -o /app/publish --no-restore

FROM mcr.microsoft.com/dotnet/runtime:8.0-noble-chiseled AS final

WORKDIR /app
COPY --from=build --chown=1654:1654 /app/publish .

USER 1654

ENTRYPOINT ["dotnet", "Worker.dll"]
