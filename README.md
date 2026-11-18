# 🌤️ Monitor de Temperatura em Tempo Real (Planilha -> API Open-Meteo)

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-orange.svg)](https://pandas.pydata.org/)
[![Open-Meteo](https://img.shields.io/badge/API-Open--Meteo-green.svg)](https://open-meteo.com/)

Este projeto automatiza a coleta de coordenadas geográficas (Latitude e Longitude) armazenadas em uma planilha pública do Google Sheets (gerada a partir de um formulário) e realiza consultas em tempo real na API do **Open-Meteo** para obter a temperatura atual de cada local cadastrado.

## 🚀 Funcionalidades

- **Integração com Google Sheets:** Consome dinamicamente os dados de um formulário exportado em formato CSV.
- **Geolocalização & Clima:** Consulta dados meteorológicos atualizados de latitude e longitude sem necessidade de chaves de API (utilizando o serviço público Open-Meteo).
- **Automação:** Pronto para ser executado em loops ou agendadores para monitoramento contínuo.

## 🛠️ Tecnologias Utilizadas

- **Python:** Linguagem base do projeto.
- **Pandas:** Para manipulação, leitura e estruturação dos dados vindos da planilha.
- **Requests:** Para realizar as requisições HTTP na API do Open-Meteo.
- **Open-Meteo API:** Provedor de dados climáticos de alta precisão e código aberto.

## 📋 Estrutura da Planilha de Entrada

A planilha lida pelo código deve conter as seguintes colunas obrigatórias:
- `Nome do local`: Nome identificador do ponto de interesse.
- `Latitude`: Coordenada de latitude (ex: `-23.55`).
- `Longitude`: Coordenada de longitude (ex: `-46.63`).

## 💻 Trecho de Código Principal

O fluxo de execução do projeto segue o seguinte pipeline:

```python
# 1. Carrega os dados coletados da planilha pública
dados_planilha = pd.read_csv(endopint_planilha)

# 2. Itera sobre cada registro e busca as informações de clima em tempo real
for indice, linha in dados_planilha.iterrows():
    parametros = {
        'latitude': linha['Latitude'],
        'longitude': linha['Longitude'],
        'current': 'temperature_2m'
    }
    resposta = requests.get(endpoint_api, params=parametros).json()
    print(f"Local: {linha['Nome do local']} | Temperatura Atual: {resposta['current']['temperature_2m']}°C")
```

## 🤝 Contribuições

Contribuições são super bem-vindas! Sinta-se à vontade para abrir uma **Issue** ou enviar um **Pull Request**.

--- 
Desenvolvido com 💙 para fins de estudo de integração de dados e APIs.
