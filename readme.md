ETL Project - API Data Extraction

Descrição

Este projeto implementa um processo ETL (Extract, Transform, Load) para extrair dados de uma API, transformá-los conforme necessário e carregá-los em um banco de dados ou outro destino de armazenamento.

Tecnologias Utilizadas

Python (para a implementação do ETL)

Requests (para consumir a API)

Pandas (para transformar os dados)

SQLAlchemy (para carregar os dados no banco de dados)

PostgreSQL/MySQL (como banco de dados destino, opcional)

Fluxo do ETL

Extração: Os dados são obtidos via requisição HTTP para a API.

Transformação: Os dados são convertidos em um formato adequado, limpando e estruturando as informações.

Carga: Os dados transformados são inseridos em um banco de dados ou salvos em um arquivo (CSV, JSON, etc.).

Como Usar

1. Configurar o ambiente

Instale as dependências necessárias:

pip install requests pandas sqlalchemy psycopg2

2. Configurar a API e Banco de Dados

Crie um arquivo .env para armazenar as credenciais:

API_URL=https://api.exemplo.com/dados
DB_CONNECTION=postgresql://usuario:senha@localhost:5432/meubanco

3. Executar o script ETL

python etl.py

Exemplo de Código

Aqui está um exemplo básico do fluxo ETL:

import requests
import pandas as pd
from sqlalchemy import create_engine
import os

# Configuração
API_URL = os.getenv("API_URL")
DB_CONNECTION = os.getenv("DB_CONNECTION")

# Extração
def extract_data():
    response = requests.get(API_URL)
    data = response.json()
    return pd.DataFrame(data)

# Transformação
def transform_data(df):
    df = df.dropna()  # Exemplo: remover valores nulos
    return df

# Carga
def load_data(df):
    engine = create_engine(DB_CONNECTION)
    df.to_sql('dados_api', engine, if_exists='replace', index=False)

if __name__ == "__main__":
    df = extract_data()
    df = transform_data(df)
    load_data(df)
    print("ETL concluído com sucesso!")

Melhorias Futuras

Agendar a execução do ETL com Apache Airflow ou Crontab.

Implementar logging para monitoramento do processo.

Criar testes unitários para validação dos dados extraídos e transformados.

Autor

Gustavo Cardoso

Licença

Este projeto está sob a licença MIT.