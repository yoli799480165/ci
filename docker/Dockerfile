FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base

FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:9.0 AS build
ARG BUILD_VERSION
ARG TARGETARCH
WORKDIR /build
COPY dotnet dotnet
WORKDIR /build/dotnet
RUN dotnet publish demo1.csproj \
	-c Release \
	-o /dist \
	-a $TARGETARCH \
    /p:AssemblyVersion=$BUILD_VERSION \
    /p:Version=$BUILD_VERSION

FROM base AS run
WORKDIR /app
COPY --from=build /dist .
ENTRYPOINT ["dotnet", "demo1.dll"]
