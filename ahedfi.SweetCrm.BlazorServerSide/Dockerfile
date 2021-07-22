#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["ahedfi.SweetCrm.BlazorServerSide/ahedfi.SweetCrm.BlazorServerSide.csproj", "ahedfi.SweetCrm.BlazorServerSide/"]
RUN dotnet restore "ahedfi.SweetCrm.BlazorServerSide/ahedfi.SweetCrm.BlazorServerSide.csproj"
COPY . .
WORKDIR "/src/ahedfi.SweetCrm.BlazorServerSide"
RUN dotnet build "ahedfi.SweetCrm.BlazorServerSide.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ahedfi.SweetCrm.BlazorServerSide.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ahedfi.SweetCrm.BlazorServerSide.dll"]