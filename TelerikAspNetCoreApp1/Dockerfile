FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["TelerikAspNetCoreApp1/TelerikAspNetCoreApp1.csproj", "TelerikAspNetCoreApp1/"]
RUN dotnet restore "TelerikAspNetCoreApp1/TelerikAspNetCoreApp1.csproj"
COPY . .
WORKDIR "/src/TelerikAspNetCoreApp1"
RUN dotnet build "TelerikAspNetCoreApp1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TelerikAspNetCoreApp1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TelerikAspNetCoreApp1.dll"]