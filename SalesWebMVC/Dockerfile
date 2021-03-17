#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:2.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:2.1 AS build
WORKDIR /src
COPY ["SalesWebMVC/SalesWebMVC.csproj", "SalesWebMVC/"]
RUN dotnet restore "SalesWebMVC/SalesWebMVC.csproj"
COPY . .
WORKDIR "/src/SalesWebMVC"
RUN dotnet build "SalesWebMVC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SalesWebMVC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SalesWebMVC.dll"]