# Monitoramento com Prometheus, Grafana e Tempo

Este repositório contém um ambiente de monitoramento baseado em Docker Compose, incluindo Prometheus, Grafana e Tempo.

## Requisitos
- Docker
- Docker Compose

## Como Clonar o Repositório
```sh
git clone <URL_DO_REPOSITORIO>
cd <NOME_DO_REPOSITORIO>
```

## Como Iniciar os Serviços
Execute o seguinte comando na raiz do repositório:
```sh
docker-compose up -d
```
Isso iniciará os serviços em segundo plano.

## Serviços e Portas

| Serviço    | Imagem                             | Porta Externa | Finalidade |
|-----------|-----------------------------------|--------------|------------|
| Tempo     | `grafana/tempo:latest`           | 14268        | Ingestão Jaeger |
|           |                                   | 3200         | Interface Tempo |
|           |                                   | 6831 (UDP)   | Protocolo Jaeger UDP |
|           |                                   | 4318         | OPENTELEMETRY HTTP |
| Prometheus | `prom/prometheus:latest`         | 9090         | Interface do Prometheus |
| Grafana   | `grafana/grafana-enterprise:latest` | 8080         | Interface do Grafana |

## Rede Utilizada
Todos os serviços utilizam a rede Docker `monitoramento`. Certifique-se de que a rede existe antes de iniciar os containers:
```sh
docker network create monitoramento
```

## Como Parar os Serviços
```sh
docker-compose down
```

## Acesso às Interfaces
- **Prometheus**: [http://localhost:9090](http://localhost:9090)
- **Grafana**: [http://localhost:8080](http://localhost:8080)
- **Tempo**: API acessível na porta `3200`

## Logs dos Serviços
Para verificar os logs de um serviço específico, use:
```sh
docker-compose logs -f <serviço>
```
Exemplo para visualizar os logs do Prometheus:
```sh
docker-compose logs -f prometheus
```

## Considerações
- O Grafana pode exigir login padrão (`admin/admin` no primeiro acesso).
- Os arquivos de configuração são montados via volumes locais, permitindo personalização.

Caso encontre problemas, verifique se as portas não estão em uso por outros serviços ou se a rede Docker está corretamente configurada.

