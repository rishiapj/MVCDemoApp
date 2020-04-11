FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["MVCDemoApp/MVCDemoApp.csproj", "MVCDemoApp/"]
RUN dotnet restore "MVCDemoApp/MVCDemoApp.csproj"
COPY . .
WORKDIR "/src/MVCDemoApp"
RUN dotnet build "MVCDemoApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MVCDemoApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MVCDemoApp.dll"]