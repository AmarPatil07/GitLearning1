FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["GitLearning/GitLearning.csproj", "GitLearning/"]
RUN dotnet restore "GitLearning/GitLearning.csproj"
COPY . .
WORKDIR "/src/GitLearning"
RUN dotnet build "GitLearning.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "GitLearning.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "GitLearning.dll"]