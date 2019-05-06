FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["WebApiGIT/WebApiGIT.csproj", "WebApiGIT/"]
RUN dotnet restore "WebApiGIT/WebApiGIT.csproj"
COPY . .
WORKDIR "/src/WebApiGIT"
RUN dotnet build "WebApiGIT.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApiGIT.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApiGIT.dll"]