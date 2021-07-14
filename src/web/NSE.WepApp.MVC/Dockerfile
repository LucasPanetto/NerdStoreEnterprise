#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["src/web/NSE.WepApp.MVC/NSE.WepApp.MVC.csproj", "src/web/NSE.WepApp.MVC/"]
RUN dotnet restore "src/web/NSE.WepApp.MVC/NSE.WepApp.MVC.csproj"
COPY . .
WORKDIR "/src/src/web/NSE.WepApp.MVC"
RUN dotnet build "NSE.WepApp.MVC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NSE.WepApp.MVC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NSE.WepApp.MVC.dll"]