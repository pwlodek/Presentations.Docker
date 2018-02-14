FROM microsoft/aspnetcore-build AS builder
WORKDIR /source
ARG CONFIG

# copy sources 
COPY . .

# restore libraries
RUN dotnet restore

# build
RUN dotnet publish --configuration ${CONFIG:-Debug} --output /app

# build runtime image
FROM microsoft/aspnetcore:latest
EXPOSE 80
WORKDIR /app
COPY --from=builder /app .
ENTRYPOINT ["dotnet", "HelloDockerApi.dll"]