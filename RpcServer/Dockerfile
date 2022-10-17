FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["RpcServer/RpcServer.csproj", "RpcServer/"]
RUN dotnet restore "RpcServer/RpcServer.csproj"
COPY . .
WORKDIR "/src/RpcServer"
RUN dotnet build "RpcServer.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RpcServer.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RpcServer.dll"]
