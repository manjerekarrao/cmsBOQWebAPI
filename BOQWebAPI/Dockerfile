FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["BOQWebAPI/BOQWebAPI.csproj", "BOQWebAPI/"]
RUN dotnet restore "BOQWebAPI/BOQWebAPI.csproj"
COPY . .
WORKDIR "/src/BOQWebAPI"
RUN dotnet build "BOQWebAPI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "BOQWebAPI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "BOQWebAPI.dll"]