# 🚀 Deploy da API

Este guia ensina como implantar a API em **servidores na nuvem** e como **containerizar** o projeto com Docker.

## 📌 1. Criando um Dockerfile

1. Crie um arquivo `Dockerfile` na raiz do projeto:
```dockerfile
# Usando imagem do .NET SDK
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app

# Copiando os arquivos para dentro do container
COPY ./ClientesAPI /app
RUN dotnet build -c Release
RUN dotnet publish -c Release -o out

# Definindo ponto de entrada
ENTRYPOINT ["dotnet", "out/ClientesAPI.dll"]
```

2. Construa e execute o container:
```sh
docker build -t clientes-api .
docker run -p 5000:5000 clientes-api
```

## 📌 2. Publicando no Railway (Fácil)
1. Crie uma conta em [https://railway.app/](https://railway.app/)
2. Faça o deploy diretamente do GitHub.

## 📌 3. Publicando no Azure
1. No **Azure Portal**, crie um **App Service**.
2. Faça o deploy via **GitHub Actions**:
```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Configurar .NET
        uses: actions/setup-dotnet@v1
        with:
          dotnet-version: 7.0
      - name: Publicar
        run: dotnet publish -c Release -o out
      - name: Deploy no Azure
        uses: azure/webapps-deploy@v2
        with:
          app-name: "clientes-api"
          package: "out"
```