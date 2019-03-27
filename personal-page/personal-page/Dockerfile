FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["personal-page/personal-page.csproj", "personal-page/"]
RUN dotnet restore "personal-page/personal-page.csproj"
COPY . .
WORKDIR "/src/personal-page"
RUN dotnet build "personal-page.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "personal-page.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "personal-page.dll"]