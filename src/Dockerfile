FROM mcr.microsoft.com/dotnet/core/sdk:3.1-bionic AS build-core

WORKDIR /app

RUN apt-get update && apt-get install -y --no-install-recommends nodejs npm
COPY ./Blog.Core/package.json ./Blog.Core/package.json
COPY ./Blog.Core/gulpfile.js ./Blog.Core/gulpfile.js
COPY ./Blog.Core/assets ./Blog.Core/assets
RUN cd Blog.Core && npm install && npm run gulp

COPY ./Blog.Core ./Blog.Core
COPY ./Blog.sln ./

RUN dotnet publish -c Release Blog.Core -o /Blog.Core

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-bionic

WORKDIR /app

COPY --from=build-core /Blog.Core .
ENTRYPOINT ["./Blog.Core"]