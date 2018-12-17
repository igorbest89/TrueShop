FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 27120
EXPOSE 44395

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["TrueShop/TrueShop.csproj", "TrueShop/"]
RUN dotnet restore "TrueShop/TrueShop.csproj"
COPY . .
WORKDIR "/src/TrueShop"
RUN dotnet build "TrueShop.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TrueShop.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TrueShop.dll"]