# Pipeline ETL com Python, POO e API REST do GitHub

Pipeline de Engenharia de Dados desenvolvido em Python utilizando a biblioteca `requests`, `pandas` e Programação Orientada a Objetos (POO) para extrair, transformar e carregar dados sobre as linguagens de programação mais utilizadas por grandes empresas de tecnologia (Amazon, Netflix e Spotify) diretamente via API do GitHub.

## Arquitetura do Projeto

```text
projeto_Requests/
├── dados/
│   ├── linguagens_amzn.csv       # Base tratada dos repositórios da Amazon
│   ├── linguagens_netflix.csv    # Base tratada dos repositórios da Netflix
│   └── linguagens_spotify.csv    # Base tratada dos repositórios do Spotify
├── amazon.csv                    # Arquivo gerado na etapa inicial de prototipagem
├── dados._repos.py               # Classe DadosRepositorios (Extração e Transformação)
├── manipula_repos.py             # Classe ManipulaRepositorios (Carga via API POST/PUT)
├── linguagens_repos_aula1.ipynb  # Notebook de exploração e testes dos endpoints
├── .gitignore                    # Exclusão do ambiente virtual e caches
└── README.md                     # Documentação do projeto
```

## Etapas do Pipeline (ETL)

1. **Extração (`GET` + Paginação + Autenticação):**
   * Consumo autenticado da API REST do GitHub (`api.github.com`) utilizando *Personal Access Token* via `headers`.
   * Iteração automática entre páginas (`?page=1...20`) para coletar todos os repositórios públicos das organizações alvo.
2. **Transformação (`JSON` → `DataFrame`):**
   * Filtragem dos campos relevantes (`name` e `language`) a partir das listas de dicionários retornadas pela API.
   * Estruturação tabular com `pandas` e exportação para arquivos `.csv`.
3. **Carregamento (`POST` + `Base64` + `PUT`):**
   * Criação automatizada de repositório de destino no GitHub via requisição `POST`.
   * Codificação binária dos arquivos `.csv` em `Base64` (`utf-8`) e envio automatizado via requisição `PUT`.

## Tecnologias Utilizadas

* **Python 3.10**
* **Requests** (requisições HTTP `GET`, `POST`, `PUT` e `DELETE`)
* **Pandas** (manipulação de DataFrames e geração de CSV)
* **Base64** (codificação de arquivos para envio via API)
* **WSL2 (Ubuntu) & VS Code**

## Como Executar

1. Clone o repositório e acesse a pasta do projeto:
   ```bash
   git clone https://github.com/CristianTI777/pipeline-api-github.git
   cd pipeline-api-github
   ```
2. Crie e ative o ambiente virtual:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install requests pandas
   ```
3. Insira seu *Personal Access Token* do GitHub na variável `self.access_token` nos arquivos de classe e execute os scripts Python.
