FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["aspnetcoreapp/aspnetcoreapp.csproj", "aspnetcoreapp/"]
RUN dotnet restore "aspnetcoreapp/aspnetcoreapp.csproj"
COPY . .
WORKDIR "/src/aspnetcoreapp"
RUN dotnet build "aspnetcoreapp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "aspnetcoreapp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "aspnetcoreapp.dll"]