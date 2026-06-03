# Vyracare

Vyracare e um ecossistema modular para clinicas de estetica, com frontend Angular, APIs .NET, templates e pipelines reutilizaveis para entrega em `dev`, `hml` e `prod`.

O foco do produto e suportar a operacao digital da clinica com uma base tecnica que permita evolucao continua, separacao por dominio e promocao controlada entre ambientes.

## Como o fluxo funciona

O fluxo de promocao atual e:

1. feature -> PR para `develop`
2. merge em `develop`
3. publish automatico em `dev`
4. criacao automatica de `release/<versionamento>`
5. PR de `develop` para `release/<versionamento>`
6. merge em `release/*`
7. CI roda novamente
8. publish automatico em `hml`
9. PR de `release/*` para `main`
10. merge em `main`
11. publish automatico em `prod`

Padrao de release:

- `release/vYYYY.MM.DD.<run_number>`

## Arquitetura

### Frontend

- `vyracare-app-shell` como host principal
- MFEs Angular carregados por `remoteEntry.js`
- `vyracare-design-system` como base compartilhada de UI
- deploy em S3 + CloudFront
- separacao entre ambiente local, `dev`, `hml` e `prod`

Arquivos de ambiente Angular:

- `environment.ts`: desenvolvimento local
- `environment.dev.ts`: ambiente `dev`
- `environment.hml.ts`: ambiente `hml`
- `environment.prod.ts`: ambiente `prod`

### Backend

- APIs .NET separadas por dominio
- organizacao interna em `vertical slice`
- runtime em AWS Lambda
- exposicao por API Gateway HTTP
- persistencia em MongoDB
- segredos em AWS Secrets Manager
- deploy independente por dominio funcional

## Repositorios principais

### Frontend

- `vyracare-app-shell`
- `vyracare-app-user-mfe`
- `vyracare-app-profile-mfe`
- `vyracare-app-dashboard-mfe`
- `vyracare-app-proceedings-mfe`
- `vyracare-design-system`

### Backend

- `vyracare-api-authentication`
- `vyracare-api-client`
- `vyracare-api-proceedings`

### Templates

- `templates-angular`
- `template-dot-net-api`

### Pipelines reutilizaveis

- `vyracare-infra-pipes-angular`
- `vyracare-infra-pipes-dot-net`

### Documentacao e especificacao

- `vyracare-spec-driven`

## URLs de acesso

### Shell

| Ambiente | URL |
| --- | --- |
| Local | [http://localhost:4200](http://localhost:4200) |
| Dev | [https://dnhcnj7sdnfel.cloudfront.net](https://dnhcnj7sdnfel.cloudfront.net) |
| HML | [https://d2ukbrzje889m2.cloudfront.net](https://d2ukbrzje889m2.cloudfront.net) |
| Prod | [https://d13ugmrrfi5a31.cloudfront.net](https://d13ugmrrfi5a31.cloudfront.net) |

### Design system

| Recurso | URL |
| --- | --- |
| Playground publicado | [https://dvgk2zjit84dn.cloudfront.net](https://dvgk2zjit84dn.cloudfront.net) |
| Storybook publicado | [https://d2pws2zjq41jau.cloudfront.net](https://d2pws2zjq41jau.cloudfront.net) |

### APIs

#### Authentication

| Ambiente | Base URL |
| --- | --- |
| Local | [http://localhost:5000/api/auth](http://localhost:5000/api/auth) |
| Dev | [https://axswteu0u1.execute-api.us-east-1.amazonaws.com/api/auth](https://axswteu0u1.execute-api.us-east-1.amazonaws.com/api/auth) |
| HML | [https://jkvfvgsw4l.execute-api.us-east-1.amazonaws.com/api/auth](https://jkvfvgsw4l.execute-api.us-east-1.amazonaws.com/api/auth) |
| Prod | [https://bj6riwfeni.execute-api.us-east-1.amazonaws.com/api/auth](https://bj6riwfeni.execute-api.us-east-1.amazonaws.com/api/auth) |

#### Client

| Ambiente | Base URL |
| --- | --- |
| Dev | [https://028k6c7rpb.execute-api.us-east-1.amazonaws.com/api/client](https://028k6c7rpb.execute-api.us-east-1.amazonaws.com/api/client) |
| HML | [https://1vd2y2p3ni.execute-api.us-east-1.amazonaws.com/api/client](https://1vd2y2p3ni.execute-api.us-east-1.amazonaws.com/api/client) |
| Prod | [https://4uh1kerr9a.execute-api.us-east-1.amazonaws.com/api/client](https://4uh1kerr9a.execute-api.us-east-1.amazonaws.com/api/client) |

#### Proceedings

| Ambiente | Base URL |
| --- | --- |
| Dev | [https://eri1s9zq97.execute-api.us-east-1.amazonaws.com/api/proceedings](https://eri1s9zq97.execute-api.us-east-1.amazonaws.com/api/proceedings) |
| HML | [https://lsh2vmjq8k.execute-api.us-east-1.amazonaws.com/api/proceedings](https://lsh2vmjq8k.execute-api.us-east-1.amazonaws.com/api/proceedings) |
| Prod | [https://ya4lnham1d.execute-api.us-east-1.amazonaws.com/api/proceedings](https://ya4lnham1d.execute-api.us-east-1.amazonaws.com/api/proceedings) |

### Swagger das APIs

As APIs publicadas expoem Swagger UI e `swagger.json` por ambiente.

#### Authentication

| Ambiente | Swagger |
| --- | --- |
| Dev | [https://axswteu0u1.execute-api.us-east-1.amazonaws.com/swagger/index.html](https://axswteu0u1.execute-api.us-east-1.amazonaws.com/swagger/index.html) |
| HML | [https://jkvfvgsw4l.execute-api.us-east-1.amazonaws.com/swagger/index.html](https://jkvfvgsw4l.execute-api.us-east-1.amazonaws.com/swagger/index.html) |
| Prod | [https://bj6riwfeni.execute-api.us-east-1.amazonaws.com/swagger/index.html](https://bj6riwfeni.execute-api.us-east-1.amazonaws.com/swagger/index.html) |

#### Client

| Ambiente | Swagger |
| --- | --- |
| Dev | [https://028k6c7rpb.execute-api.us-east-1.amazonaws.com/swagger/index.html](https://028k6c7rpb.execute-api.us-east-1.amazonaws.com/swagger/index.html) |
| HML | [https://1vd2y2p3ni.execute-api.us-east-1.amazonaws.com/swagger/index.html](https://1vd2y2p3ni.execute-api.us-east-1.amazonaws.com/swagger/index.html) |
| Prod | [https://4uh1kerr9a.execute-api.us-east-1.amazonaws.com/swagger/index.html](https://4uh1kerr9a.execute-api.us-east-1.amazonaws.com/swagger/index.html) |

#### Proceedings

| Ambiente | Swagger |
| --- | --- |
| Dev | [https://eri1s9zq97.execute-api.us-east-1.amazonaws.com/swagger/index.html](https://eri1s9zq97.execute-api.us-east-1.amazonaws.com/swagger/index.html) |
| HML | [https://lsh2vmjq8k.execute-api.us-east-1.amazonaws.com/swagger/index.html](https://lsh2vmjq8k.execute-api.us-east-1.amazonaws.com/swagger/index.html) |
| Prod | [https://ya4lnham1d.execute-api.us-east-1.amazonaws.com/swagger/index.html](https://ya4lnham1d.execute-api.us-east-1.amazonaws.com/swagger/index.html) |

## Onde aprofundar

Para detalhes tecnicos e operacionais:

- `vyracare-spec-driven/01-foundation/ai-dlc.md`
- `vyracare-spec-driven/01-foundation/repository-landscape.md`
- `vyracare-spec-driven/02-architecture/frontend-architecture.md`
- `vyracare-spec-driven/02-architecture/backend-architecture.md`
- `vyracare-spec-driven/02-architecture/environment-strategy.md`
- `vyracare-spec-driven/03-delivery/angular-pipelines.md`
- `vyracare-spec-driven/03-delivery/dotnet-pipelines.md`
- `vyracare-spec-driven/05-operations/runbooks.md`

## Convencao de commits

Os repositorios da organizacao seguem o padrao de mensagens de commit em portugues.

Exemplos:

- `feat: adiciona ambiente de homologacao`
- `fix: corrige rotas de swagger da autenticacao`
- `docs: atualiza matriz de ambientes e acessos`

## Observacoes

- URLs de CloudFront e API Gateway podem mudar se um recurso for recriado.
- O shell e o ponto principal de acesso dos ambientes publicados.
- O padrao atual privilegia consistencia de arquitetura, automacao de promocao e isolamento por ambiente.
