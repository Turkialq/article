FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 5103
EXPOSE 7066

# Use the .NET 8 SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["ReportService.csproj", "./"]
RUN dotnet restore "./ReportService.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "ReportService.csproj" -c Release -o /app/build

# Publish the application
FROM build AS publish
RUN dotnet publish "ReportService.csproj" -c Release -o /app/publish

# Build the runtime image using the base stage
FROM base AS final
WORKDIR /app

ENTRYPOINT ["dotnet", "ReportService.dll"]