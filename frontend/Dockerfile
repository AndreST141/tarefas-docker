# Image do node
FROM node:22-alpine

# Define o diretório de trabalho dentro do container
WORKDIR /app

# Copia os arquivos de dependências
COPY package*.json ./

# Instala
RUN npm install

# Copia o restante do código
COPY . .

# Expo a porta padrão do vite
EXPOSE 8080

# Comando para iniciar o frontend
CMD ["npm", "run", "dev", "--", "--host", "--port", "8080"]