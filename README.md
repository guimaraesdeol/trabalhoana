# trabalhoana
TRABALHO ESTATISTICA DESCRITIVA, CÓDIGO BASE EM R - DOCUMENTAÇÃO EM BREVE - LIBRARY SCAT


Código:


# Passo 1: Verificando e instalando (se necessário) pacote caret
if (!require(caret)) {
  install.packages("caret")
  library(caret)
}

# Passo 2: Carregando o conjunto de dados scat
data(scat, package = "caret")
dados <- as.data.frame(scat)

# Passo 3: Criando tabela de ocorrências para a variável Species
ocorrenciaSpecies <- table(dados$Species)

# Passo 4: Plotando tabela de ocorrências para Species
barplot(ocorrenciaSpecies, xlab = 'Espécies', ylab = 'Ocorrências')

# Passo 5: Agrupando classes menos significativas da tabela de ocorrências
# Inicializando a nova tabela e a soma das ocorrências menos significativas
tabela <- 0
soma = 0
b = 1

# Agrupando as ocorrências
for (i in 1:length(ocorrenciaSpecies)) {
  if (ocorrenciaSpecies[i] > 0) { # Usando o critério de relevância fornecido
    tabela[b] <- ocorrenciaSpecies[i]
    names(tabela)[b] <- names(ocorrenciaSpecies)[i]
    b = b + 1
  } else {
    soma = soma + ocorrenciaSpecies[i]
  }
}

# Adicionando a classe "Outros"
# tabela[length(tabela) + 1] = soma
# names(tabela)[length(tabela)] <- "Outros"

# Passo 6: Plotando a nova tabela de ocorrências incluindo a classe "Outros"
cores <- c(rainbow(length(tabela) - 1), "gray")
barplot(tabela, xlab = "Espécies", ylab = "Ocorrências", col = cores)

# Passo 7: Calculando frequências relativas
freqRelSpecies = round(100 * prop.table(tabela), 2)
nomesPizza = paste(names(tabela), "-", freqRelSpecies, "%", sep = "")
pie(tabela, labels = nomesPizza, col = cores)
