FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["CoreMvcDocker/CoreMvcDocker.csproj", "CoreMvcDocker/"]
RUN dotnet restore "CoreMvcDocker/CoreMvcDocker.csproj"
COPY . .
WORKDIR "/src/CoreMvcDocker"
RUN dotnet build "CoreMvcDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CoreMvcDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreMvcDocker.dll"]