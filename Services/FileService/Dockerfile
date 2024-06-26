FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 5057
EXPOSE 7271

# Use the .NET 8 SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["FileService.csproj", "./"]
RUN dotnet restore "./FileService.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "FileService.csproj" -c Release -o /app/build

# Publish the application
FROM build AS publish
RUN dotnet publish "FileService.csproj" -c Release -o /app/publish

# Build the runtime image using the base stage
FROM base AS final
WORKDIR /app

ENTRYPOINT ["dotnet", "FileService.dll"]