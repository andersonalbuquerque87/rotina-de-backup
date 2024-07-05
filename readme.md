#A documentação fornece orientações detalhadas sobre como configurar, testar e garantir a eficácia de um backup de rotina.

## Script de Backup Automatizado
O script a seguir cria um backup do diretório "/opt" e salva no diretório "/backup/opt". O backup é nomeado com a data atual e os logs são salvos em "/var/log/backup_opt.log".

### Explicação

1. **Definindo Variáveis**
    - SOURCE_DIR="/opt": Define o diretório de origem que será copiado.
    - DEST_DIR="/backup/opt": Define o diretório de destino onde o backup será armazenado.
    - BACKUP_NAME="backup_$(date +%Y%m%d).tar.gz": Define o nome do arquivo de backup, incluindo a data atual no formato AAAAMMDD.
    - LOG_FILE="/var/log/backup_opt.log": Define o caminho do arquivo de log.

2. **Iniciando o Backup**
    - echo "$(date '+%Y-%m-%d %H:%M:%S') - Iniciando o backup do diretório $SOURCE_DIR para $DEST_DIR/$BACKUP_NAME" >> $LOG_FILE: Registra a mensagem de início do backup no log.

3. **Criando o Backup**
    - tar -czf $DEST_DIR/$BACKUP_NAME $SOURCE_DIR 2>> $LOG_FILE: Cria o arquivo de backup em formato tar.gz. Se houver erros, eles são registrados no arquivo de log.

4. **Verificando o Resultado do Backup**
    - if [ $? -eq 0 ]; then: Verifica se o comando anterior (tar) foi bem-sucedido.
    - echo "$(date '+%Y-%m-%d %H:%M:%S') - Backup concluído com sucesso" >> $LOG_FILE: Se o backup for bem-sucedido, registra uma mensagem de sucesso no log.
    - else echo "$(date '+%Y-%m-%d %H:%M:%S') - Backup não concluído" >> $LOG_FILE: Se o backup falhar, registra uma mensagem de erro no log.

#### Agendando o Script com Cron

Para agendar o script para execução automática, podemos usar o "cron". Siga os passos abaixo:

1. **Tornar o Script Executável**
sudo chmod +x /usr/local/bin/rotinabackup.sh

2. **Editar o Crontab do Usuário Root**
sudo crontab -e

3. **Adicionar a Linha de Agendamento**
Adicione a seguinte linha ao arquivo do crontab para executar o script todos os dias às 2:00 da manhã:
0 2 * * * /usr/local/bin/rotinabackup.sh

4. **Salvar e Sair**
No editor nano, pressione "Ctrl + O", Enter para salvar e "Ctrl + X" para sair.

5. **Reiniciar o Serviço Cron**
sudo systemctl restart cron

6. **Verificar o Status do Serviço Cron**
sudo systemctl status cron

##### Verificação de Erros

Se o cron job não estiver funcionando, verifique os logs do cron para encontrar erros específicos:
sudo grep CRON /var/log/syslog
