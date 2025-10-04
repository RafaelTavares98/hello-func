# Teste local Azure Functions Hello World (Python)

## Objetivo
Usar o template do Azure Core Tools para subir uma Function HTTP de forma rápida.

## Pré-requisitos
- Azure Functions Core Tools v4 
- Python instalado
- curl disponível para teste

## 1. Iniciar o projeto
```bash
func init . --python # cria a estrutura base de Function configurado para Python.
```

Arquivos gerados: function_app.py, host.json, local.settings.json, requirements.txt, .gitignore, .vscode/

## 2. Criar a função HTTP
```bash
func new --name HelloWorldFunc --template "HTTP trigger" # inicia o assistente de criação de função em HTTP
```
Selecione a opção 2 (ANONYMOUS) para Auth Level.

## 3. Executar localmente
Execute
```bash
func start
```

## 4. Testar

- Abra outro terminal e execute:
  ```bash
  curl "http://localhost:7071/api/HelloWorldFunc?name=Rafael"
  ```
- Ou acesse no navegador:
  ```bash
  http://localhost:7071/api/HelloWorldFunc?name=Rafael
  ```

Resposta esperada:

"Hello, Rafael. This HTTP triggered function executed successfully."

## 5. Estrutura de diretórios
.
├── function_app.py
├── host.json
├── local.settings.json
├── requirements.txt
├── .gitignore
└── .vscode/

