FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["TesteImpressora/TesteImpressora.csproj", "TesteImpressora/"]
RUN dotnet restore "TesteImpressora/TesteImpressora.csproj"
COPY . .
WORKDIR "/src/TesteImpressora"
RUN dotnet build "TesteImpressora.csproj" -c Release -r linux-arm -o /app

FROM build AS publish
RUN dotnet publish "TesteImpressora.csproj" -c Release -r linux-arm -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TesteImpressora.dll"]
