# download_enem
Download files from Enem

library(dplyr)

library(data.table)

temp <- tempfile() #criar arquivo temprario
download.file("https://download.inep.gov.br/microdados/microdados_enem_2019.zip",temp)#definir o site e o arquivo temporario
data <- read.table(unz(temp, "DADOS/MICRODADOS_ENEM_2019.csv"),
                   sep= ";", fill = TRUE,header=TRUE)%>% # incidar separador, preenchimento e existencia de titulo 
         filter(TP_DEPENDENCIA_ADM_ESC==1&CO_UF_ESC==21)#filtrar pelo estado e escolas federais
unlink(temp)#limpar arquivos temporarios

write.csv(data, file="ENEM2019.csv")#salva o arquivo resumido no diretorio de trabalho

# Altere o ano para outras analise (2019 por 2018 ou 2017 etc)
# Para analisar todas as escolas do esta retire "TP_DEPENDENCIA_ADM_ESC==1&"
