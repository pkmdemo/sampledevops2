#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["SampleDevOps2/SampleDevOps2.csproj", "SampleDevOps2/"]
RUN dotnet restore "SampleDevOps2/SampleDevOps2.csproj"
COPY . .
WORKDIR "/src/SampleDevOps2"
RUN dotnet build "SampleDevOps2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SampleDevOps2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SampleDevOps2.dll"]