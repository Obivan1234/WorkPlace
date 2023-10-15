FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WorkPlace.API.csproj", "WorkPlace/"]
RUN dotnet restore "WorkPlace.API.csproj"
COPY . .
WORKDIR "/src/WorkPlace"
RUN dotnet build "WorkPlace.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WorkPlace.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WorkPlace.API.dll"]