#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see http://aka.ms/containercompat 

FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 59423
EXPOSE 44372

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY Echo/Echo.csproj Echo/
RUN dotnet restore Echo/Echo.csproj
COPY . .
WORKDIR /src/Echo
RUN dotnet build Echo.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Echo.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Echo.dll"]
