FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["IOTdevice.csproj", "./"]
RUN dotnet restore "IOTdevice.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "IOTdevice.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "IOTdevice.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "IOTdevice.dll"]
