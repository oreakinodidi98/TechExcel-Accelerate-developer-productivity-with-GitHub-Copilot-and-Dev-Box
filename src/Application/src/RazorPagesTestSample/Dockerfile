# Use the official .NET 8 SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /app

# Copy the csproj file and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the remaining files and build the application
COPY . ./
RUN dotnet publish -c Release -o out

# Use the official .NET 8 ASP.NET runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Copy the build output from the build stage
COPY --from=build-env /app/out .

# Set the environment variable for the ASP.NET Core HTTP port
ENV ASPNETCORE_HTTP_PORTS=80

# Specify the entry point for the application
ENTRYPOINT ["dotnet", "RazorPagesTestSample.dll"]