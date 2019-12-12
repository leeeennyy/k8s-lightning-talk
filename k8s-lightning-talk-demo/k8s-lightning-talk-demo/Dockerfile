#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["k8s-lightning-talk-demo/k8s-lightning-talk-demo.csproj", "k8s-lightning-talk-demo/"]
RUN dotnet restore "k8s-lightning-talk-demo/k8s-lightning-talk-demo.csproj"
COPY . .
WORKDIR "/src/k8s-lightning-talk-demo"
RUN dotnet build "k8s-lightning-talk-demo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "k8s-lightning-talk-demo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "k8s-lightning-talk-demo.dll"]