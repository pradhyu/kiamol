FROM mcr.microsoft.com/dotnet/core/sdk:3.1.301-alpine AS builder

WORKDIR /src
COPY src/WebPingOperator.Model/WebPingOperator.Model.csproj ./WebPingOperator.Model/
COPY src/WebPingOperator.WebPingerController/WebPingOperator.WebPingerController.csproj ./WebPingOperator.WebPingerController/

WORKDIR /src/WebPingOperator.WebPingerController
RUN dotnet restore

COPY src /src
RUN dotnet publish -c Release -o /out WebPingOperator.WebPingerController.csproj

# app image
FROM mcr.microsoft.com/dotnet/core/runtime:3.1.5-alpine

WORKDIR /app
ENTRYPOINT ["dotnet", "WebPingOperator.WebPingerController.dll"]

COPY --from=builder /out/ .