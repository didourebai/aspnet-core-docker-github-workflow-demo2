#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER app
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["aspnet-core-docker-github-workflow-demo2/aspnet-core-docker-github-workflow-demo2/aspnet-core-docker-github-workflow-demo2.csproj", "aspnet-core-docker-github-workflow-demo2/aspnet-core-docker-github-workflow-demo2/"]
RUN dotnet restore "./aspnet-core-docker-github-workflow-demo2/aspnet-core-docker-github-workflow-demo2/./aspnet-core-docker-github-workflow-demo2.csproj"
COPY . .
WORKDIR "/src/aspnet-core-docker-github-workflow-demo2/aspnet-core-docker-github-workflow-demo2"
RUN dotnet build "./aspnet-core-docker-github-workflow-demo2.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "./aspnet-core-docker-github-workflow-demo2.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspnet-core-docker-github-workflow-demo2.dll"]