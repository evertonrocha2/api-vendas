# Documentação Microserviços
https://claude.ai/code/artifact/2c541174-0b49-486d-9ee2-1682e91b8daf

# Documentação implementação Docker GUIA
https://claude.ai/code/artifact/a5f3c8e5-81de-4791-a16c-a71d4aa45f0f

# Documentação implementação Kubernetes GUIA
https://claude.ai/code/artifact/68cd2944-af3d-430f-8e6f-ea27c4186982

# Aluno
Everton Rocha (PREENCHER nome completo) - Matricula: PREENCHER

# fornecedores-service (porta 8084)
Novo microsservico criado a partir do clientes-service. Endpoints:

- GET /fornecedores
- GET /fornecedores/{id} (404 se nao existir)
- POST /fornecedores (201 com o objeto criado)
- GET /fornecedores/produtos (lista de produtos obtida do produtos-service via Feign)

Configuracao externalizada em config-repo/fornecedores-service.properties (e o perfil docker em fornecedores-service-docker.properties).
O auth-service passou da porta 8084 para a 8086 para liberar a 8084 ao fornecedores-service.

Pelo gateway (8085) as rotas exigem JWT. Para obter um token:

1. POST http://localhost:8085/auth-service/usuarios com {"nome": "...", "email": "...", "senha": "..."}
2. POST http://localhost:8085/auth-service/usuarios/login com {"email": "...", "senha": "..."}, copie o token
3. GET http://localhost:8085/fornecedores-service/fornecedores com o header Authorization: Bearer <token>
