#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["RemoteFile/RemoteFile.csproj", "RemoteFile/"]
RUN dotnet restore "RemoteFile/RemoteFile.csproj"
COPY . .
WORKDIR "/src/RemoteFile"
RUN dotnet build "RemoteFile.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RemoteFile.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RemoteFile.dll"]