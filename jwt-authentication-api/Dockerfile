FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY WebApi.sln .
COPY WebApi/WebApi.csproj ./src/
COPY WebApi.sln ./src/
RUN dotnet restore ./src/WebApi.csproj

# copy everything else and build app
COPY WebApi/. ./src/
WORKDIR /app/src
RUN dotnet publish WebApi.csproj -c Release -o out

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS runtime
WORKDIR /app
COPY --from=build /app/src/out ./
ENTRYPOINT ["dotnet", "WebApi.dll"]
