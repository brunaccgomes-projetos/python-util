# 📑 Organizar Variáveis de Ambiente
Sim, separar as configurações sensíveis ou reutilizáveis em um arquivo à parte é uma melhor prática de desenvolvimento. 
Isso melhora a organização, facilita a manutenção e aumenta a segurança dos dados sensíveis, como as chaves de acesso AWS. 
Aqui está como você pode fazer isso:

---

## 1. Separar Configurações em um Arquivo de Variáveis
Crie um arquivo chamado, por exemplo, config.py para armazenar as configurações:
 
 ```bash
## config.py

# Configurações AWS
AWS_ACCESS_KEY = 'sua_chave_de_acesso'
AWS_SECRET_KEY = 'sua_chave_secreta'
BUCKET_NAME = 'ds-aih-bronze'

# Diretório local para arquivos temporários
LOCAL_TEMP_DIR = './temp/'
```

---

## 2. Como Importar no Script de Ingestão
No seu script principal, você pode importar essas configurações para utilizá-las:

 ```bash
## ingestion.py

from config import AWS_ACCESS_KEY, AWS_SECRET_KEY, BUCKET_NAME, LOCAL_TEMP_DIR

# Use as variáveis no script
print(f"Enviando dados para o bucket: {BUCKET_NAME}")
```

---

## 3. Alternativa para Maior Segurança: Variáveis de Ambiente
Para evitar salvar chaves de acesso no código, utilize variáveis de ambiente. Isso é mais seguro, especialmente quando o projeto for compartilhado ou enviado para produção.

### Passo 1: Configurar Variáveis de Ambiente
Defina as variáveis no sistema operacional ou em um arquivo .env:

No terminal (Linux/Mac):

 ```bash
## bash

export AWS_ACCESS_KEY="sua_chave_de_acesso"
export AWS_SECRET_KEY="sua_chave_secreta"
export BUCKET_NAME="ds-aih-bronze"
export LOCAL_TEMP_DIR="./temp/"

```
No Windows (PowerShell):

 ```bash
## powershell

$env:AWS_ACCESS_KEY="sua_chave_de_acesso"
$env:AWS_SECRET_KEY="sua_chave_secreta"
$env:BUCKET_NAME="ds-aih-bronze"
$env:LOCAL_TEMP_DIR="./temp/"
```


### Passo 2: Usar Variáveis no Script
Instale a biblioteca python-dotenv para carregar as variáveis de um arquivo .env:

 ```bash
## bash

pip install python-dotenv
```

Crie um arquivo .env com as chaves: .env

 ```bash
## makefile

AWS_ACCESS_KEY=sua_chave_de_acesso
AWS_SECRET_KEY=sua_chave_secreta
BUCKET_NAME=ds-aih-bronze
LOCAL_TEMP_DIR=./temp/
```
No script Python:

 ```bash
## python

from dotenv import load_dotenv
import os

# Carregar variáveis do arquivo .env
load_dotenv()

AWS_ACCESS_KEY = os.getenv('AWS_ACCESS_KEY')
AWS_SECRET_KEY = os.getenv('AWS_SECRET_KEY')
BUCKET_NAME = os.getenv('BUCKET_NAME')
LOCAL_TEMP_DIR = os.getenv('LOCAL_TEMP_DIR')

print(f"Usando o bucket: {BUCKET_NAME}")
```

---


## 4. Vantagens de Usar Configurações Separadas
- **Segurança:** As credenciais sensíveis não ficam expostas no código principal.
- **Reutilização:** Configurações podem ser usadas por diferentes scripts.
- **Manutenção:** Alterar configurações é mais simples e centralizado.
