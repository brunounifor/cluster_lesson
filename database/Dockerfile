# Usa a imagem oficial do MongoDB como base
FROM mongo:6.0

# Define variáveis de ambiente para o MongoDB
ENV MONGO_INITDB_ROOT_USERNAME=root
ENV MONGO_INITDB_ROOT_PASSWORD=example
ENV MONGO_INITDB_DATABASE=todo

# Define o diretório onde o MongoDB armazenará os dados
VOLUME /data/db

# Exponha a porta padrão do MongoDB
EXPOSE 27017

# Comando para iniciar o MongoDB
CMD ["mongod"]
