#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.
# Используйте базовый образ SDK для сборки и публикации приложения
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["../WebAPIRestAPI.csproj", "./"]
RUN dotnet restore "WebAPIRestAPI.csproj"

COPY . .
WORKDIR "/src/WebAPIRestAPI"
RUN dotnet build "../WebAPIRestAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "../WebAPIRestAPI.csproj" -c Release -o /app/publish

# Используйте базовый образ runtime для запуска приложения
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAPIRestAPI.dll"]