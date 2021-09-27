#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["CoreDockerWebDemo2/CoreDockerWebDemo2.csproj", "CoreDockerWebDemo2/"]
RUN dotnet restore "CoreDockerWebDemo2/CoreDockerWebDemo2.csproj"
COPY . .
WORKDIR "/src/CoreDockerWebDemo2"
RUN dotnet build "CoreDockerWebDemo2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CoreDockerWebDemo2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CoreDockerWebDemo2.dll"]