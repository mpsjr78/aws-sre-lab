# Estágio 1: Build da aplicação Angular
# Usando Node 12 do ECR Public (compatível com o Angular 8 do projeto)
FROM public.ecr.aws/docker/library/node:12-stretch AS builder

WORKDIR /app

# Instalar dependências e CLI do Angular
COPY package.json .
# O parametro --unsafe-perm resolve problemas de permissão do usuário 'node' no build
RUN npm install --unsafe-perm
RUN npm install -g @angular/cli@8.3.29 --unsafe-perm

# Copiar código e compilar
COPY . .
RUN ng build --prod

# Estágio 2: Servidor Web
# ATUALIZADO: Usando Nginx Stable Alpine do ECR Public (Leve e disponível)
FROM public.ecr.aws/docker/library/nginx:stable-alpine

LABEL maintainer="voce@exemplo.com"

# Copiar os artefatos compilados do estágio anterior
COPY --from=builder /app/dist/yelb-ui/ /usr/share/nginx/html/

EXPOSE 80