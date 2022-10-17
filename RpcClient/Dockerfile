FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["RpcClient/RpcClient.csproj", "RpcClient/"]
RUN dotnet restore "RpcClient/RpcClient.csproj"
COPY . .
WORKDIR "/src/RpcClient"
RUN dotnet build "RpcClient.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RpcClient.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RpcClient.dll"]
