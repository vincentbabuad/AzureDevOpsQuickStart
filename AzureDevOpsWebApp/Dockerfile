FROM mcr.microsoft.com/dotnet/runtime:3.1 AS base
WORKDIR /app
EXPOSE 62210
EXPOSE 44306

FROM mcr.microsoft.com/dotnet/core/sdk:3.1  AS build
WORKDIR /src
COPY ["AzureDevOpsWebApp/AzureDevOpsWebApp.csproj", "AzureDevOpsWebApp/"]
RUN dotnet restore "AzureDevOpsWebApp/AzureDevOpsWebApp.csproj"
COPY . .
WORKDIR "/src/AzureDevOpsWebApp"
RUN dotnet build "AzureDevOpsWebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AzureDevOpsWebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AzureDevOpsWebApp.dll"]
