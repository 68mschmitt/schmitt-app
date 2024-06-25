FROM mcr.microsoft.com/dotnet/sdk:8.0 AS builder
WORKDIR /app

COPY *.csproj ./
RUN dotnet restore

COPY . .

RUN dotnet publish -c Release -o out

FROM ubuntu.azurecr.io/dotnet-aspnet:8.0-24.04_stable

WORKDIR /app
COPY --from=builder /app/out ./

ENV PORT 8080
EXPOSE 8080

ENTRYPOINT ["dotnet", "/app/API.dll"]