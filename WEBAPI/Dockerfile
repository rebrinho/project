FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 62504
EXPOSE 44345

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY WEBAPI/WEBAPI.csproj WEBAPI/
RUN dotnet restore WEBAPI/WEBAPI.csproj
COPY . .
WORKDIR /src/WEBAPI
RUN dotnet build WEBAPI.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WEBAPI.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WEBAPI.dll"]
