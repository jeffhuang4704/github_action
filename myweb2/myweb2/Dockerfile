#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["myweb2/myweb2.csproj", "myweb2/"]
RUN dotnet restore "myweb2/myweb2.csproj"
COPY . .
WORKDIR "/src/myweb2"
RUN dotnet build "myweb2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "myweb2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "myweb2.dll"]