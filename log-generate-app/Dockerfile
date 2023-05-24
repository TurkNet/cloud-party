FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY . . 
RUN dotnet restore
RUN dotnet build "log-generate-app.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "log-generate-app.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .

ENTRYPOINT ["dotnet", "log-generate-app.dll"]
