# 🚀 Deploying the API

This guide explains how to deploy the API on **cloud servers** and how to **containerize** the project using Docker.

## 📌 1. Creating a Dockerfile

1. Create a `Dockerfile` in the project's root directory:
```dockerfile
# Using .NET SDK image
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app

# Copying files into the container
COPY ./ClientesAPI /app
RUN dotnet build -c Release
RUN dotnet publish -c Release -o out

# Setting entry point
ENTRYPOINT ["dotnet", "out/ClientesAPI.dll"]
```

2. Build and run the container:
```sh
docker build -t clientes-api .
docker run -p 5000:5000 clientes-api
```

## 📌 2. Deploying to Railway (Easy)
1. Create an account at [https://railway.app/](https://railway.app/)
2. Deploy directly from GitHub.

## 📌 3. Deploying to Azure
1. In **Azure Portal**, create an **App Service**.
2. Deploy using **GitHub Actions**:
```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup .NET
        uses: actions/setup-dotnet@v1
        with:
          dotnet-version: 7.0
      - name: Publish
        run: dotnet publish -c Release -o out
      - name: Deploy to Azure
        uses: azure/webapps-deploy@v2
        with:
          app-name: "clientes-api"
          package: "out"
```