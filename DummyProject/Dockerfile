# Build stage
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:8.0-bookworm-slim AS build
ARG TARGETARCH
WORKDIR /app
COPY . /app

RUN dotnet restore DummyProject.csproj -a $TARGETARCH

RUN dotnet publish DummyProject.csproj -c Release --no-restore -o out -a $TARGETARCH /p:SelfContained=false /p:PublishSingleFile=true

# Runtime stage
FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/aspnet:8.0-bookworm-slim
WORKDIR /app
COPY --from=build /app/out .

ENTRYPOINT ["./DummyProject"]