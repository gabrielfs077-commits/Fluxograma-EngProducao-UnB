# MVP: Sistema de Apoio à Decisão (SAD) - Trilha EPR
**Universidade de Brasília (UnB) | Engenharia de Produção**
*Projeto de Apresentação para a disciplina de Sistemas de Suporte à Decisão (SSD)*

---

## O Problema
O planeamento semestral de matrículas na Engenharia de Produção é um problema clássico de otimização multicritério. O aluno precisa cruzar três dimensões complexas:
1. **Intenção de Carreira:** Escolher disciplinas aderentes ao seu perfil (Logística, Pesquisa Operacional, Finanças, etc.).
2. **Restrições Lógicas:** Cumprir a cadeia rígida de pré-requisitos (ex: não é possível cursar Pesquisa Operacional sem aprovação prévia em Cálculo e Estatística).
3. **Capacidade de Carga:** Respeitar o tempo disponível do estudante no semestre.

## A Solução
Este MVP apresenta um "Motor de Otimização Semântica" operado via Google Colab. Diferente de buscadores tradicionais por palavra-chave, este SAD utiliza Processamento de Linguagem Natural (NLP) para entender ementas e aplicar lógicas restritivas em tempo real.

Funcionalidades Principais (Highlights da Apresentação)
- **Motor NLP (Similaridade de Cossenos):** Transforma textos de ementas em vetores (`sentence-transformers`) e calcula o ângulo matemático de proximidade com o objetivo do aluno, superando o *overfitting* lexical.
- **Validador de Restrições (Trator Regex):** Um motor de regras booleanas que varre o histórico do aluno e barra disciplinas cujos pré-requisitos não foram atendidos.
- **Problema da Mochila (Knapsack):** Algoritmo guloso que preenche a carga horária livre do aluno com as disciplinas de maior *Score* de IA.
- **Gap Analysis (Visão de Futuro):** Recurso de simulação ("What-If") que mostra quais disciplinas perfeitas para a carreira estão bloqueadas e quais matérias o aluno precisa cursar para libertá-las.
- **Dashboard Interativo:** UI amigável rodando nativamente no Colab via `ipywidgets`.

---

Tecnologias Utilizadas
- **Python 3**
- **Pandas:** Para ETL, limpeza e deduplicação do dataset (CSV).
- **Sentence Transformers (`paraphrase-multilingual-MiniLM-L12-v2`):** Para geração de embeddings vetoriais.
- **IPyWidgets:** Para construção da interface gráfica interativa.
- **Expressões Regulares (Regex):** Para o *parsing* da lógica de pré-requisitos.

---

## Como Rodar o MVP (Guia para o Apresentador)

1. **Preparação:** Tenha o arquivo `disciplinas.csv` atualizado no seu computador.
2. **Passo 1 (Instalações):** Execute a primeira célula do Google Colab para instalar as bibliotecas necessárias.
3. **Passo 2 (Cérebro e ETL):** Execute a segunda célula. Um botão de upload aparecerá. Envie o `disciplinas.csv`. Aguarde o sistema carregar a IA e higienizar a base.
4. **Passo 3 (Dashboard):** Execute a terceira célula para renderizar a Interface de Usuário.

---

## Cenários de Teste para a Banca (Showroom)

Durante a apresentação, simule estes perfis alterando o campo **Histórico** no Dashboard:

### 1. O Calouro (Em branco)
- **Histórico:** *(Deixe vazio)*
- **O que mostrar:** O sistema bloqueia todas as disciplinas de engenharia aplicada e recomenda apenas introduções.

### 2. O Sobrevivente do Ciclo Básico (Fim do 4º Semestre)
- **Histórico:** `MAT0025, MAT0026, MAT0027, IFD0171, IFD0173, IFD0175, MAT0031, CIC0007, EST0023`
- **O que mostrar:** A base de Exatas e Estatística abre portas. Se escolhermos "Pesquisa Operacional", o sistema recomenda as primeiras matérias específicas. Mostre a inteligência do sistema adicionando `ADM0023` ao histórico para ver a grade mudar em tempo real.

### 3. A Simulação de Flexibilidade (Gap Analysis)
- **O que mostrar:** Desligue a Checkbox *"Aplicar Trava Rígida de Pré-requisitos"*. O sistema mostrará a grade "Ideal" apontando com a tag `[⚠️ FALTAM PRÉ-REQUISITOS]` o que o aluno não tem. Ligue a trava novamente, e essas matérias descerão automaticamente para a secção de Análise de Lacunas (Visão de Futuro).

---
*Desenvolvido para a disciplina de Sistemas de Suporte à Decisão (SSD) - 2026*
