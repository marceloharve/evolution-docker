# Evolution API - Docker Setup

Sistema WhatsApp multi-instância usando Evolution API + Docker.

## 🚀 Quick Start

### 1. Iniciar containers

```bash
cd evolution-docker
docker-compose up -d
```

### 2. Verificar status

```bash
docker-compose ps
docker-compose logs -f evolution-api
```

### 3. Acessar UI

- **Manager UI:** http://localhost:8080/manager
- **API Base:** http://localhost:8080
- **Documentação Swagger:** http://localhost:8080/docs

### 4. Parar containers

```bash
docker-compose down
# ou para remover volumes também:
docker-compose down -v
```

## 📊 Containers

| Container | Porta | Descrição |
|-----------|-------|-----------|
| evolution-api | 8080 | Evolution API (WhatsApp) v2.2.3+ |
| postgresql | 5432 | Banco de dados PostgreSQL |
| redis | 6379 | Cache e filas |

## 🔧 Configuração

Edite `.env` para ajustar:
- `EVOLUTION_API_KEY`: Chave de autenticação da API
- `POSTGRES_PASSWORD`: Senha do PostgreSQL  
- `WEBHOOK_URL`: URL do backend Python

**Importante:** A Evolution API requer PostgreSQL como DATABASE_PROVIDER. MongoDB não é suportado.

## 🧪 Testar

```python
# No backend Python
python -m tests.test_evolution_multiuser
```

## 📝 Logs

```bash
# Evolution API
docker-compose logs -f evolution-api

# PostgreSQL
docker-compose logs -f postgresql

# Todos
docker-compose logs -f
```

## 🔄 Atualizar Evolution

```bash
docker-compose pull evolution-api
docker-compose up -d evolution-api
```

## ⚠️ Troubleshooting

### Porta 8080 já em uso
```bash
# Windows
netstat -ano | findstr :8080
taskkill /PID <PID> /F

# Ou altere a porta no docker-compose.yml
```

### Containers não iniciam
```bash
docker-compose down -v
docker-compose up -d
```

### Erro "Database provider invalid"
- Certifique-se que `DATABASE_PROVIDER=postgresql` está configurado
- A Evolution API não suporta MongoDB diretamente
- Verifique se o PostgreSQL está rodando

### Resetar tudo
```bash
docker-compose down -v
docker volume prune
docker-compose up -d
```

## 📚 Referências

- [Documentação Evolution API](https://doc.evolution-api.com/)
- [GitHub Evolution API](https://github.com/EvolutionAPI/evolution-api)

## 🚀 Deploy Railway (Produção)

Veja arquivo `railway.toml` para configuração de produção.
