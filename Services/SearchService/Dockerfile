FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 5248
EXPOSE 7272

# Use the .NET 8 SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["SearchService.csproj", "./"]
RUN dotnet restore "./SearchService.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "SearchService.csproj" -c Release -o /app/build

# Publish the application
FROM build AS publish
RUN dotnet publish "SearchService.csproj" -c Release -o /app/publish

# Build the runtime image using the base stage
FROM base AS final
WORKDIR /app

ENTRYPOINT ["dotnet", "SearchService.dll"]