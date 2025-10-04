# Azure Functions Hello World (Python)

## Objetivo
Reproduzir o exercício da aula: criar, rodar localmente e testar uma Azure Function HTTP.

## Pré-requisitos
- Azure Functions Core Tools v4 (verificar com func --version)
- Python instalado
- curl disponível para teste

## 1. Iniciar o projeto
func init . --python

Arquivos gerados: function_app.py, host.json, local.settings.json, requirements.txt, .gitignore, .vscode/

## 2. Criar a função HTTP
func new --name HelloWorldFunc --template "HTTP trigger"
Selecione a opção 2 (ANONYMOUS) para Auth Level.

## 3. Executar localmente
Modo padrão:
func start

Modo em segundo plano:
nohup func start > func.log 2>&1 &
tail -f func.log
Parar o processo:
pkill -f "func start"

## 4. Testar
curl "http://localhost:7071/api/HelloWorldFunc?name=Rafael"
Resposta esperada:
Hello, Rafael. This HTTP triggered function executed successfully.

## 5. Estrutura de diretórios
.
├── function_app.py
├── host.json
├── local.settings.json
├── requirements.txt
├── .gitignore
└── .vscode/

## 6. Dicas rápidas
- Auth ANONYMOUS é útil para testes. Em produção use FUNCTION.
- Se a porta 7071 estiver ocupada, pare o processo ou mude WEBSITE_PORT.
- Logs: tail -f func.log
- local.settings.json é local e já está no .gitignore.

## 7. Publicar no Azure (opcional)
az login
az account set --subscription "<SUBSCRIPTION_ID>"
RESOURCE_GROUP="rg-hello-func"
LOCATION="brazilsouth"
STORAGE="st$RANDOM$RANDOM"
APP="hello-func-app-$RANDOM"
az group create -n $RESOURCE_GROUP -l $LOCATION
az storage account create -g $RESOURCE_GROUP -n $STORAGE -l $LOCATION --sku Standard_LRS
az functionapp create -g $RESOURCE_GROUP --consumption-plan-location $LOCATION --runtime python --functions-version 4 --name $APP --storage-account $STORAGE
func azure functionapp publish $APP
curl "https://$APP.azurewebsites.net/api/HelloWorldFunc?name=Rafael"

## 8. Erros comuns
- func: command not found → reinstalar Core Tools v4
- 403/401 → função não está com AuthLevel=ANONYMOUS
- Timeout → verificar se host está rodando e URL correta

## 9. Limpeza
pkill -f "func start"
az group delete -n $RESOURCE_GROUP --yes --no-wait
