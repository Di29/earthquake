FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["wes/wes.csproj", "wes/"]
RUN dotnet restore "wes/wes.csproj"
COPY . .
WORKDIR "/src/wes"
RUN dotnet build "wes.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "wes.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "wes.dll"]