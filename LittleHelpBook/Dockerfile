FROM mvpstudio/base:v1 AS base
ENV ASPNETCORE_URLS=http://+:80  

WORKDIR /app
EXPOSE 80

# https://docs.microsoft.com/en-us/dotnet/core/install/linux-package-manager-debian10
RUN apt-get install wget && \
wget -O- https://packages.microsoft.com/keys/microsoft.asc | \
gpg --dearmor > microsoft.asc.gpg && \
mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/ && \
wget https://packages.microsoft.com/config/debian/10/prod.list && \
mv prod.list /etc/apt/sources.list.d/microsoft-prod.list && \
chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg && \
chown root:root /etc/apt/sources.list.d/microsoft-prod.list && \
apt-get update && echo "Y" | apt-get install dotnet-runtime-3.1 && \
apt-get install aspnetcore-runtime-3.1

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["LittleHelpBook.csproj", ""]
RUN dotnet restore "./LittleHelpBook.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "LittleHelpBook.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LittleHelpBook.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .

ENTRYPOINT ["dotnet", "LittleHelpBook.dll"]
