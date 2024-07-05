#!/bin/bash

SOURCE_DIR="/opt"
DEST_DIR="/backup/opt"
BACKUP_NAME="backup_$(date +%Y%m%d).tar.gz"
LOG_FILE="/var/log/backup_opt.log"

# Start Backup
echo "$(date '+%Y-%m-%d %H:%M:%S') - Iniciando o backup do diretório $SOURCE_DIR para $DEST_DIR/$BACKUP_NAME" >> $LOG_FILE

# Criando o Backup
tar -czf $DEST_DIR/$BACKUP_NAME $SOURCE_DIR 2>> $LOG_FILE

if [ $? -eq 0 ]; then
	echo "$(date '+%Y-%m-%d %H:%M:%S') - Backup concluído com sucesso" >> $LOG_FILE
else
	echo "$(date '+%Y-%m-%d %H:%M:%S') - Backup não concluído" >> $LOG_FILE
fi
