FROM microsoft/dotnet:2.0-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.0-sdk AS build
WORKDIR /src
COPY *.sln ./
COPY ConsulTest.Client/ConsulTest.Client.csproj ConsulTest.Client/
COPY ConsulTest.Library/ConsulTest.Library.csproj ConsulTest.Library/
RUN dotnet restore
COPY . .
WORKDIR /src/ConsulTest.Client
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ConsulTest.Client.dll"]
