﻿FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Server/SeniorProj.Server.csproj", "Server/"]
COPY ["Client/SeniorProj.Client.csproj", "Client/"]
COPY ["Shared/SeniorProj.Shared.csproj", "Shared/"]
RUN dotnet restore "Server/SeniorProj.Server.csproj"
COPY . .
WORKDIR "/src/Server"
RUN dotnet build "SeniorProj.Server.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SeniorProj.Server.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .

COPY ["Server/users.db", "/app"]
COPY ["Server/users.db", "/app/publish"]

ENTRYPOINT ["dotnet", "SeniorProj.Server.dll"]
