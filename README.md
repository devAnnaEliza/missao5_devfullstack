# missao_nv5
# Universidade Estácio de Sá - Polo Santa Cruz/Rio de Janeiro 
# Anna Eliza de Almeida Silva mat: 202208837093 // 2022.3
# Desenvolvimento Full Stack // Missão prática nível 5 - Colocando tudo em ordem e guardando 

# Título da missão - Implementação de um programa para manipular dados de um arquivo de texto e visualizá-los em um histograma e uma nuvem de palavras.
# Objetivo da missão do nível 5 - Gerar dados de testes, gravar e recuperar dados de arquivos textos, manipular os dados para visualizá-los em um histograma e em uma nuvem de palavras, 
# implementar um programa para gerar dados com nomes de pessoas e respectivas pontuações, gravar em um arquivo, recuperar os dados do arquivo, visualizar os dados das pontuações das pessoas em um histograma e em uma nuvem de palavras.

-------------------------------------------------------------------------------------------
# Instalação das bibliotecas
!pip install faker
!pip install num2words
!pip install WordCloud
!pip install datetime
------------------------------------------------------------------------------
# Bibliotecas importadas 
from faker import Faker 
from datetime import datetime 
from wordcloud import WordCloud 
from num2words import num2words
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
--------------------------------------------------------------------------------------------
# Dados aleatórios gerados
dados_alt = Faker('pt_BR') 
dados_list = [] 
notas_list = [] 
nomes_list = [] 

# Teste da criação do arquivo
%%writefile dadosnv5.txt 
Aluno: Otávio Cavalcanti - Nota: 7
Aluno: João Lucas Rocha - Nota: 9
Aluno: Luigi Correia - Nota: 6
Aluno: Ana Lívia Costa - Nota: 4
Aluno: Paulo Dias - Nota: 10
Aluno: Fernando Caldeira - Nota: 5
Aluno: Luiz Otávio da Rosa - Nota: 7
Aluno: Enzo Barros - Nota: 2
Aluno: Laís Monteiro - Nota: 3
Aluno: Lavínia da Conceição - Nota: 9
Aluno: Emanuel Silveira - Nota: 7
Aluno: Rafaela Martins - Nota: 10
Aluno: Marcela Cardoso - Nota: 8
Aluno: Bianca Porto - Nota: 3
Aluno: Ana Laura Cunha - Nota: 10
------------------------------------------------------------------------------------------------------
# Dados gravados 
for i in range(15): 
   
   
   dados = ('Aluno:' + dados_alt.name() + ' - ' + 'Nota: ' + str(dados_alt.random_int(1,10))) 
   dados_list.append(dados) 
-------------------------------------------------------------------------------------------------------
# Abrindo arquivo .txt
with open('dadosnv5.txt', 'w', encoding='utf-8') as arquivo:
    for valor in dados_list: 
     arquivo.write(valor + '\n')
--------------------------------------------------------------------------------------------------------
# Recuperando e lendo as linhas do arquivo
with open('dadosnv5.txt', 'r', encoding='utf-8') as arquivo_recuperar: 
  for i in range (len(dados_list)): 
    ler = arquivo_recuperar.readline() 
    separar_notas = ler.split(' ') 
    nota = int(separar_notas[-1]) 
    notas_list.append(nota) 
    nomes_list_2 = num2words(nota, lang= 'pt_BR')
    nomes_list.append(nomes_list_2)
    nomes_list_str = (' ').join(nomes_list) 
----------------------------------------------------------------------------------------------------
# Criação do histograma 
plt.title('Histograma das pontuações')
plt.xlabel('Pontuações')
plt.ylabel('Probabilidade')
plt.xlim(-0.5,10.5) 
plt.hist(notas_list, bins = np.arange(-0.5,11), density = True, rwidth = 0.75) 
plt.show()
-------------------------------------------------------------------------------------------------------------
# Criação da nuvem de palavras com WordCloud
nuvem_palavras = WordCloud(background_color = 'Black', width = 800, height = 400).generate(nomes_list_str) 
plt.imshow(nuvem_palavras, interpolation = 'bilinear') 
plt.axis("off") 
nuvem_palavras.to_file("Nuvem de palavras.png") 

----------------------------------------------------------------------------------------------------------------
# Análise e conclusão da missão 

# Qual a importância de manipular arquivos de texto? Permite que o desenvolvedor aprenda a lidar com um tipo de arquivo que não está acostumado a lidar normalmente, ampliando seu conhecimento e sua experiência.
# Qual a importância de visualizar os dados em um histograma? Facilita o entendimento de quem não está acostumado com o mundo da programação.
# O que significa a visualização por nuvem de palavras? Assim como o histograma, facilita a compreensão e também nos permite ver os dados representados de forma diferente.
