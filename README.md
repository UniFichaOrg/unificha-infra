# UniFicha Infra

Este repositório contém a infraestrutura e artefatos de suporte do projeto UniFicha, incluindo configurações Docker, esquema Prisma e código gerado para uso pelo backend.

## Visão geral

- Infraestrutura containerizada com `docker-compose` para facilitar o ambiente de desenvolvimento e testes.
- Banco de dados PostgreSQL inicializado pelos scripts em `docker/postgres/init.sql`.
- Esquema e migrações do Prisma em `prisma/` e cliente Prisma gerado em `generated/prisma`.

## Estrutura do repositório

- `docker-compose.yml` — orquestração dos containers usados pelo projeto.
- `docker/` — recursos e inicializadores para containers (ex.: `docker/postgres/init.sql`).
- `prisma/` — esquema Prisma e migrações.
- `generated/prisma/` — código TypeScript gerado pelo Prisma (cliente, tipos, modelos).

## Pré-requisitos

- Docker e Docker Compose instalados.
- Node.js (recomendado 18+) e gerenciador de pacotes (`npm`, `pnpm` ou `yarn`) se for executar scripts locais.

## Configuração e execução (desenvolvimento)

1. Subir os serviços básicos (Postgres, etc) com Docker Compose:

```bash
docker-compose up -d
```

2. (Opcional) Verificar logs do Postgres:

```bash
docker-compose logs -f postgres
```

3. Gerar o cliente Prisma (se alterar o schema):

```bash
npx prisma generate
```

4. Executar migrações (modo desenvolvimento):

```bash
npx prisma migrate dev
```

Observação: dependendo de como o backend estiver organizado (scripts/serviço), você pode precisar executar os comandos acima dentro do container da aplicação ou no host; ajuste usando `docker compose run --rm <service>` quando necessário.

## Desenvolvimento local do backend

- O cliente Prisma gerado fica em `generated/prisma`. Importe-o no seu código TypeScript/Node.js para acessar o banco.
- Se o projeto tiver scripts no `package.json`, use `npm install` e os scripts fornecidos para iniciar o servidor ou rodar testes.

## Migrações e banco de dados

- As migrações estão em `prisma/migrations/` e o esquema em `prisma/schema.prisma`.
- Para aplicar migrações em um ambiente já em produção ou CI, prefira `npx prisma migrate deploy`.

## Scripts úteis (exemplos)

```bash
# Subir infra
docker-compose up -d

# Gerar cliente Prisma
npx prisma generate

# Rodar migrações no dev
npx prisma migrate dev

# Parar e remover containers
docker-compose down
```

## Contribuição

- Abra issues para bugs e solicitações de melhoria.
- Envie pull requests com descrições claras e, quando aplicável, atualize as migrações do Prisma.

## Contato

Para dúvidas sobre a infraestrutura, contate os mantenedores do projeto.
