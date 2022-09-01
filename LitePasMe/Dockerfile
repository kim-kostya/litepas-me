FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["LitePasMe/LitePasMe.csproj", "LitePasMe/"]
RUN dotnet restore "LitePasMe/LitePasMe.csproj"
COPY . .
WORKDIR "/src/LitePasMe"
RUN dotnet build "LitePasMe.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LitePasMe.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LitePasMe.dll"]
