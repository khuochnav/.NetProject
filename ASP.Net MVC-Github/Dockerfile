#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["ASP.Net MVC-Github/ASP.Net MVC-Github.csproj", "ASP.Net MVC-Github/"]
RUN dotnet restore "ASP.Net MVC-Github/ASP.Net MVC-Github.csproj"
COPY . .
WORKDIR "/src/ASP.Net MVC-Github"
RUN dotnet build "ASP.Net MVC-Github.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ASP.Net MVC-Github.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ASP.Net MVC-Github.dll"]