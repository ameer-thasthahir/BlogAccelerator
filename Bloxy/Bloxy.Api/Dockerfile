FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Bloxy.Api/Bloxy.Api.csproj", "Bloxy.Api/"]
RUN dotnet restore "Bloxy.Api/Bloxy.Api.csproj"
COPY . .
WORKDIR "/src/Bloxy.Api"
RUN dotnet build "Bloxy.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Bloxy.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Bloxy.Api.dll"]