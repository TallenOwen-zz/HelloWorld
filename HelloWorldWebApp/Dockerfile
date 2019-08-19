FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["HelloWorld/HelloWorldWebApp/HelloWorldWebApp.csproj", "HelloWorld/HelloWorldWebApp/"]
RUN dotnet restore "HelloWorld/HelloWorldWebApp/HelloWorldWebApp.csproj"
COPY . .
WORKDIR "/src/HelloWorld/HelloWorldWebApp"
RUN dotnet build "HelloWorldWebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloWorldWebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloWorldWebApp.dll"]