# https://hub.docker.com/_/microsoft-dotnet
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY ./samples/aspnetapp/*.sln .
COPY ./samples/aspnetapp/aspnetapp/*.csproj ./aspnetapp/
RUN dotnet restore

# copy everything else and build app
COPY ./samples/aspnetapp/* ./aspnetapp/
WORKDIR /source
RUN dotnet publish -c release -o ./samples/aspnetapp/aspnetapp/ --no-restore

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /aspnetapp
COPY --from=build ./aspnetapp ./
ENTRYPOINT ["dotnet", "aspnetapp.dll"]
