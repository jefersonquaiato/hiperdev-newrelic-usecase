FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/ObservabilityAPI.csproj", "src/"]
RUN dotnet restore "src/ObservabilityAPI.csproj"
COPY . .
WORKDIR "/src/src"
RUN dotnet build "ObservabilityAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ObservabilityAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ObservabilityAPI.dll"]