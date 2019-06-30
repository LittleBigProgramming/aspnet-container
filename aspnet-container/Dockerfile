FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY aspnet-container/aspnet-container.csproj aspnet-container/
RUN dotnet restore aspnet-container/aspnet-container.csproj
COPY . .
WORKDIR /src/aspnet-container
RUN dotnet build aspnet-container.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish aspnet-container.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "aspnet-container.dll"]
