FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 49158
EXPOSE 44313

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["DatingApp.API/DatingApp.API.csproj", "DatingApp.API/"]
RUN dotnet restore "DatingApp.API/DatingApp.API.csproj"
COPY . .
WORKDIR "/src/DatingApp.API"
RUN dotnet build "DatingApp.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DatingApp.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DatingApp.API.dll"]