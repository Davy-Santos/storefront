# STOREFRONT

## 🛍️Microsserviço Storefront

Este projeto é um Microsserviço Storefront desenvolvido como parte do bootcamp "Primeiros Passos com Java" da Digital Innovation One (DIO).
Ele atua como a camada de vitrine ou interface de loja, sendo responsável pela listagem e compra de produtos, e se comunica com o microsserviço Warehouse (estoque) para verificar a disponibilidade e registrar compras.

## 🛠️ Tecnologias Utilizadas

O projeto foi construído utilizando o ecossistema Java/Spring:

🔹Linguagem: Java 21

🔹Framework: Spring Boot 3.x

🔹Gerenciador de Dependências: Gradle (Kotlin DSL - KTS)

🔹Persistência: Spring Data JPA

🔹Banco de Dados: H2 (em memória, para desenvolvimento)

🔹Mensageria: RabbitMQ (para comunicação assíncrona com o Warehouse)

🔹Containerização: Docker e Docker Compose

🔹Outros: Lombok, MapStruct, SpringDoc (Swagger UI)

## ⚙️ Arquitetura e Comunicação
O microsserviço Storefront se comunica com o Warehouse de duas maneiras principais:

🔹 **Comunicação Síncrona (HTTP)**

Usada para obter informações detalhadas de produtos (como quantidade em estoque) do Warehouse através de uma chamada HTTP.

URL Base do Warehouse: http://warehouseapp:8080/warehouse

🔹 **Comunicação Assíncrona (RabbitMQ)**

Utilizada para enviar notificações de compra (purchase) para o Warehouse, permitindo atualização de estoque de forma desacoplada.

Fila: product.change.availability.queue

## 🚀 Como Executar o Projeto

Este projeto é configurado para execução via Docker Compose, o que simplifica o gerenciamento das dependências (como o Warehouse e o RabbitMQ).

## 🧩 Pré-requisitos

Você deve ter instalado na sua máquina:

🔹Docker

🔹Docker Compose

## 🪜 Passos

**1. Clonar o Repositório**
```
git clone https://github.com/seuusuario/storefront.git
```

**2. Configurar a Rede Externa**

É necessário que a rede externa ecommerce-net já exista, conforme definido no docker-compose.yml.

Se ainda não a criou, execute:
```
docker network create ecommerce-net
```

**3. Executar o Docker Compose**

No diretório raiz do projeto, execute:

```
docker-compose up --build
```


O serviço ficará acessível em:
👉 http://localhost:8081

## 📝 Endpoints (API)

A documentação completa da API estará disponível via Swagger UI após a inicialização do serviço:

🔗 Swagger UI: http://localhost:8081/storefront/swagger-ui.html

## 📦 ProductController

  | Método |	Endpoint | Descrição | Status de Retorno |
  | ------ | ----------| --------- |:-----------------:|
  | POST	 | /products | Cria um novo produto no catálogo.| 201 Created |
  | POST	 | /products/{id}/purchase | Registra a compra de um produto (via RabbitMQ). | 204 No Content |
 | GET	 | /products | Lista todos os produtos ativos no catálogo. | 200 OK |
 | GET	 | /products/{id} |Retorna detalhes de um produto, incluindo estoque do Warehouse. | 200 OK |

## ⚙️ Detalhes de Configuração

|Configuração | Valor |
| ----------- | :---: |
|Context Path |	/storefront|
|Porta	      | 8081  |

## 🗃️ Banco de Dados H2 (Desenvolvimento)

Para fins de desenvolvimento, o projeto utiliza o H2 Database em memória — os dados são perdidos a cada reinicialização do serviço.

🔗 Console H2: http://localhost:8081/storefront/h2-console

| Configuração | Valor|
| ------------ | :--:|
|JDBC URL: | jdbc:h2:mem:storefront |
|Username: | sa |
|Password: | (vazio) |

## 💻 Desenvolvimento e Debug

O docker-compose.yml e o build.gradle.kts foram configurados para facilitar o desenvolvimento.

## 🔥 Hot Reload

O spring-boot-devtools está habilitado e configurado para reiniciar automaticamente ao detectar mudanças nos arquivos montados como volume:

volumes:

  🔹 .:/storefront:z

## 🐞 Debug Remoto

A porta 5006 está mapeada para a porta de debug padrão do Java (5005) dentro do contêiner.

Você pode anexar seu IDE (IntelliJ, VS Code, etc.) ao endpoint:
```
localhost:5006
```

Trecho do docker-compose.yml:

```
ports:
  - "8081:8081"
  - "5006:5005"  # Porta de debug remoto
volumes:
  - .:/storefront:z # Volume para sincronizar arquivos
  ```

## 🤝 Contribuições

🔹Sinta-se à vontade para:

🔹Sugerir melhorias ✨

🔹Corrigir bugs 🐛

🔹Adicionar novos recursos 🚀
