FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebFilterMidleware/WebFilterMidleware.csproj", "WebFilterMidleware/"]
RUN dotnet restore "WebFilterMidleware/WebFilterMidleware.csproj"
COPY . .
WORKDIR "/src/WebFilterMidleware"
RUN dotnet build "WebFilterMidleware.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebFilterMidleware.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebFilterMidleware.dll"]
