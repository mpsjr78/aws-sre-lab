# Estágio 1: Build da aplicação Angular (Usando Node do espelho da AWS)
FROM public.ecr.aws/docker/library/node:12.22.12 AS builder

WORKDIR /app

# Instalar dependências e CLI do Angular
COPY package.json .
RUN npm install
RUN npm install -g @angular/cli@8.3.29

# Copiar código e compilar
COPY . .
RUN ng build --prod

# Estágio 2: Servidor Web (Usando Nginx do espelho da AWS)
FROM public.ecr.aws/docker/library/nginx:1.17.10

# Metadados (substituindo o comando MAINTAINER que estava deprecated no log)
LABEL maintainer="voce@exemplo.com"

# Copiar os artefatos compilados do estágio anterior
COPY --from=builder /app/dist/yelb-ui/ /usr/share/nginx/html/

# Configuração customizada do Nginx (se houver no repositório)
# COPY nginx-custom.conf /etc/nginx/conf.d/default.conf

EXPOSE 80