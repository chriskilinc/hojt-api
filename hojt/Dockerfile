FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["./hojt.csproj", "src/"]
RUN dotnet restore "src/hojt.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "hojt.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "hojt.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "hojt.dll"]