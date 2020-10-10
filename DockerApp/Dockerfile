
FROM mcr.microsoft.com/dotnet/core/sdk:latest AS build
WORKDIR /src
COPY ["*.csproj", "./"]
RUN dotnet restore 
COPY . .
RUN dotnet build -c Release 
RUN dotnet publish -c Release -o /dist


FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS final
WORKDIR /app
EXPOSE 80
EXPOSE 443
ENV ASPNETCORE_ENVIRONMENT=Production
ENV ConnectionStrings:SqlConnection="Productiondb"
COPY --from=build /dist .
ENTRYPOINT ["dotnet", "DockerApp.dll"]