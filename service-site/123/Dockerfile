FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["123/123.csproj", "123/"]
RUN dotnet restore "123/123.csproj"
COPY . .
WORKDIR "/src/123"
RUN dotnet build "123.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "123.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "123.dll"]