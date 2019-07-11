FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
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
