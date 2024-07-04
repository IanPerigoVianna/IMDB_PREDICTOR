README: Como Executar o Script para Previsão da Nota do IMDb
Este guia fornece instruções sobre como executar o script Python para prever a nota do IMDb de um filme com base em suas características. O script utiliza um modelo de machine learning pré-treinado, juntamente com uma função de preprocessamento para preparar os dados de entrada.

Passos Iniciais
Clonar o Repositório
Clone o repositório:

Abra um terminal ou prompt de comando e execute o seguinte comando para clonar o repositório:

bash
Copiar código
git clone (https://github.com/IanPerigoVianna/IMDB_PREDICTOR.git)


Navegue até o diretório do projeto:

Após clonar o repositório, navegue até o diretório onde o projeto foi clonado:

bash
Copiar código
cd nome_do_repositorio
Substitua nome_do_repositorio pelo nome do diretório onde o repositório foi clonado.

Instalação dos Requisitos
Instale as bibliotecas necessárias:

No mesmo terminal ou prompt de comando, instale as bibliotecas necessárias especificadas no arquivo requirements.txt. Certifique-se de estar no diretório raiz do projeto onde o arquivo requirements.txt está localizado:

bash
Copiar código
pip install -r requirements.txt
Isso garantirá que todas as dependências do projeto sejam instaladas corretamente.

Execução do Script
Copie o Código:

Copie o seguinte código e salve em um arquivo Python, por exemplo, predict_imdb_rating.py.

python
Copiar código
import pandas as pd
import cloudpickle as pickle

 Carregar o scaler, o modelo, as colunas do conjunto de treinamento e os vencedores do Oscar
with open('scaler.pkl', 'rb') as f:
    scaler = pickle.load(f)

with open('regressor.pkl', 'rb') as f:
    regressor = pickle.load(f)

with open('X_columns.pkl', 'rb') as f:
    X_columns = pickle.load(f)

with open('oscar_winners.pkl', 'rb') as f:
    oscar_winner_names = pickle.load(f)

# Carregar as funções serializadas
with open('check_oscar_winners.pkl', 'rb') as f:
    check_oscar_winners = pickle.load(f)

with open('preprocess_input.pkl', 'rb') as f:
    preprocess_input = pickle.load(f)

 Novo input, Adicione o dicionário conforme modelo abaixo do filme que você quer fazer a previsão
new_input = {
    'Series_Title': 'The Shawshank Redemption',
    'Released_Year': '1994',
    'Certificate': 'A',
    'Runtime': '142 min',
    'Genre': 'Drama',
    'Overview': 'Two imprisoned men bond over a number of years, finding solace and eventual redemption through acts of common decency.',
    'Meta_score': 80.0,
    'Director': 'Frank Darabont',
    'Star1': 'Tim Robbins',
    'Star2': 'Morgan Freeman',
    'Star3': 'Bob Gunton',
    'Star4': 'William Sadler',
    'No_of_Votes': 2343110,
    'Gross': '28,341,469'
}

 Preprocessar o novo input
processed_input = preprocess_input(new_input, scaler, X_columns, oscar_winner_names)

 Fazer a previsão
prediction = regressor.predict(processed_input)
print(f'Predicted IMDB Rating: {prediction[0]}')
Execute o Script:

No mesmo terminal ou prompt de comando, navegue até o diretório onde o arquivo predict_imdb_rating.py está localizado e execute o seguinte comando:

bash
Copiar código
python predict_imdb_rating.py
Explicação dos Componentes do Script
Carregar Modelos e Funções:
O script começa carregando o modelo de regressão, o scaler para normalização dos dados, as colunas do conjunto de treinamento, e os vencedores do Oscar a partir dos arquivos .pkl.

Novo Input:
Um exemplo de novo input é definido com as características do filme. Este dicionário deve ser ajustado conforme necessário para prever a nota de outros filmes.

Preprocessamento:
A função preprocess_input é utilizada para preprocessar o novo input. Esta função normaliza os dados e realiza outras transformações necessárias para que o modelo de regressão possa fazer a previsão corretamente.

Fazer a Previsão:
O input preprocessado é então passado para o modelo de regressão para prever a nota do IMDb.

Observações
Certifique-se de que os arquivos .pkl necessários estão na mesma pasta do script Python.
Ajuste o novo input conforme necessário para prever a nota de diferentes filmes.
Se houver problemas na execução do script, verifique se todos os pacotes necessários estão instalados corretamente e se os arquivos .pkl estão presentes no diretório correto.
