FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["WebAppDocker.csproj", "WebAppDocker/"]
RUN dotnet restore "WebAppDocker/WebAppDocker.csproj"
WORKDIR "/src/WebAppDocker"
COPY . .
RUN dotnet build "WebAppDocker.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebAppDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAppDocker.dll"]