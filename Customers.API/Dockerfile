FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

WORKDIR /app

COPY ["Customers.API.csproj", "Customers.API/"]

RUN dotnet restore "Customers.API/Customers.API.csproj"

COPY "." "Customers.API/"

WORKDIR "/app/Customers.API"

RUN dotnet build "Customers.API.csproj" -c Release -o /app/build

# publish the API
FROM build AS publish
RUN dotnet publish "Customers.API.csproj" -c Release -o /app/publish

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0

WORKDIR /app
EXPOSE 80
#EXPOSE 443

COPY --from=publish /app/publish .
ENTRYPOINT [ "dotnet", "Customers.API.dll" ]