FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
RUN curl -sL https://deb.nodesource.com/setup_10.x |  bash -
RUN apt-get install -y nodejs

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["DevSpacesTooLongTest/DevSpacesTooLongTest.csproj", "DevSpacesTooLongTest/"]

RUN dotnet restore "DevSpacesTooLongTest/DevSpacesTooLongTest.csproj"
COPY . .
WORKDIR "/src/DevSpacesTooLongTest"
RUN dotnet build "DevSpacesTooLongTest.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DevSpacesTooLongTest.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DevSpacesTooLongTest.dll"]