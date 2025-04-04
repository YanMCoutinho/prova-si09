#dockerfile to build a dotnet .90 blazorwasm app
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Copy the solution and projects
COPY prova.sln . 
COPY prova/ prova/

# Restore dependencies
RUN dotnet restore prova.sln

RUN dotnet publish prova/prova.csproj -c Release -o /app/publish --no-restore && ls /app/publish

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final
WORKDIR /app
EXPOSE 7175

COPY --from=build /app/publish .

# Run the app
ENTRYPOINT ["dotnet", "prova.dll"]