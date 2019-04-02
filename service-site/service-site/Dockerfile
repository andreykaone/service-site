FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["service-site/service-site.csproj", "service-site/"]
RUN dotnet restore "service-site/service-site.csproj"
COPY . .
WORKDIR "/src/service-site"
RUN dotnet build "service-site.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "service-site.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "service-site.dll"]