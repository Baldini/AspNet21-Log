FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 64146
EXPOSE 44389

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY AspNet21-Log/AspNet21-Log.csproj AspNet21-Log/
RUN dotnet restore AspNet21-Log/AspNet21-Log.csproj
COPY . .
WORKDIR /src/AspNet21-Log
RUN dotnet build AspNet21-Log.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish AspNet21-Log.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AspNet21-Log.dll"]
