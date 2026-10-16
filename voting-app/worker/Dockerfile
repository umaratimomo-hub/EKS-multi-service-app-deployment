FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /src
COPY Worker.csproj ./
RUN dotnet restore
COPY . .
RUN dotnet publish -c Release -o /app/publish --no-restore

FROM mcr.microsoft.com/dotnet/runtime:7.0 AS final

WORKDIR /app
COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "Worker.dll"]
