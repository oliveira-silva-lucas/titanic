# 🚢 Titanic – Previsão de Sobrevivência

Este projeto utiliza o dataset clássico do Titanic para explorar técnicas de **engenharia de variáveis** e **modelagem preditiva** com `scikit-learn`. O objetivo é prever quais passageiros sobreviveram ao naufrágio, aplicando transformações consistentes e avaliando modelos com validação cruzada.

---

## 🎯 Objetivos
- Explorar e preparar os dados do Titanic.  
- Criar variáveis derivadas que aumentem o poder preditivo.  
- Construir pipelines de transformação com `FunctionTransformer` e `ColumnTransformer`.  
- Avaliar diferentes modelos de classificação (linear e árvore).  
- Comparar desempenho com validação cruzada de 10 folds.  
- Entender fatores socioeconômicos relacionados à sobrevivência.  

---

## ⚙️ Pipeline de Pré-processamento

O pipeline final foi construído para garantir **reprodutibilidade e escalabilidade**:

1. **Engenharia de variáveis (FunctionTransformer)**  
   - Criação de novas features como `Mulher`, `Preco_por_Pessoa`, `Pessoas_por_Familia`, `Acompanhado` e interações (`Idade, Sexo, Classe e Preço por Pessoa`).  
   - Tratamento de valores ausentes em `Age` com médias condicionadas por sexo e classe.  
   - Simplificação da variável `Cabin` para apenas a letra inicial.

2. **Transformações (ColumnTransformer)**  
   - **OneHotEncoder** aplicado às variáveis categóricas (`Embarked`, `Cabin`).  

3. **Modelo final (Pipeline)**  
   - Encadeamento das etapas: `FunctionTransformer` → `ColumnTransformer` → Modelo (Logistic Regression ou RandomForest).  
   - Isso garante que todo o fluxo de preparação e modelagem seja reproduzível em qualquer conjunto de dados.

---

## 🤖 Modelagem

Dois modelos foram avaliados:

- **Modelo Linear – Logistic Regression**  
  - Utilizado como baseline para classificação binária.  
  - Hiperparâmetros ajustados via `GridSearchCV`.  
  - Melhor acurácia média em validação cruzada (10 folds): **0.8271**  

- **Modelo em Árvore – RandomForestClassifier**  
  - Modelo baseado em árvores de decisão, robusto a variáveis em diferentes escalas.  
  - Hiperparâmetros final (`max_depth=10`, `min_samples_leaf=1`, `min_samples_split=5`, `n_estimators=600`).  
  - Melhor acurácia média em validação cruzada (10 folds): **0.8373**  

---

## 📊 Resultados

O pipeline automatizado reproduziu o dataset manual criado anteriormente, garantindo consistência nas transformações.  
Na modelagem, o **RandomForest** apresentou desempenho superior ao modelo linear, confirmando a vantagem de modelos de árvore para este tipo de problema.  

Além dos resultados técnicos, a análise socioeconômica mostrou que fatores como **sexo, classe social, idade e companhia** foram determinantes para a sobrevivência: mulheres, crianças e passageiros da 1ª classe ou com maior poder aquisitivo tiveram taxas de sobrevivência mais altas, enquanto homens, idosos e passageiros da 3ª classe ou viajando sozinhos apresentaram maior risco de morte.  

---
