FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY Background/*.csproj ./Background/

RUN dotnet restore

# copy everything else and build app
COPY Background/. ./Background/

WORKDIR /app/Background
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime
WORKDIR /app

COPY --from=build /app/Background/out ./
ENTRYPOINT ["dotnet", "Background.dll"]
