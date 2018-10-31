#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 64891
EXPOSE 44307

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY ["WindowsDockerDemo/WindowsDockerDemo.csproj", "WindowsDockerDemo/"]
RUN dotnet restore "WindowsDockerDemo/WindowsDockerDemo.csproj"
COPY . .
WORKDIR "/src/WindowsDockerDemo"
RUN dotnet build "WindowsDockerDemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WindowsDockerDemo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WindowsDockerDemo.dll"]