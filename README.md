# DDD Architecture Boilerplate

Boilerplate para aplicações Java baseadas em **Domain-Driven Design (DDD)** e **Monólito Modular** usando Spring Boot 3.

## 🏗️ Arquitetura

Este projeto implementa um **Monólito Modular** seguindo os princípios de DDD, onde cada módulo representa um contexto delimitado (bounded context) com suas próprias regras de domínio.

### Estrutura do Projeto

```
ddd-arch/
├── common/              # Biblioteca comum (submodule)
├── infrastructure/      # Infraestrutura compartilhada (submodule)
└── [seus-modulos]/     # Módulos de domínio específicos
```

### Módulos Base

#### 🔧 Common Library
Biblioteca fundamental com componentes base para DDD:
- **Domain**: Entidades, agregados, eventos e value objects
- **Exceptions**: Sistema estruturado de exceções
- **Security**: Contexto de usuário e autorização
- **Logging**: Logger específico para domínio

#### 🏭 Infrastructure
Infraestrutura compartilhada com Spring Boot:
- **Config**: Configurações de segurança, mapeamento e web
- **Events**: Publisher de eventos de domínio
- **Exception Handling**: Tratamento global de exceções

## 🚀 Quick Start

### Pré-requisitos
- Java 17+
- Maven 3.6+
- Git

### 1. Clone o Repositório
```bash
git clone <seu-repositorio>
cd ddd-arch
```

### 2. Inicialize os Submódulos
```bash
git submodule init
git submodule update
```

### 3. Build do Projeto
```bash
mvn clean install
```

## 📦 Criando um Novo Módulo de Domínio

### 1. Estrutura Recomendada
```
seu-modulo/
├── src/main/java/com/sakai/seumodulo/
│   ├── domain/
│   │   ├── model/          # Entidades e agregados
│   │   ├── service/        # Serviços de domínio
│   │   ├── repository/     # Interfaces de repositório
│   │   └── event/          # Eventos de domínio
│   ├── application/
│   │   ├── service/        # Serviços de aplicação
│   │   ├── dto/            # DTOs
│   │   └── usecase/        # Casos de uso
│   ├── infrastructure/
│   │   ├── persistence/    # Implementação JPA
│   │   ├── messaging/      # Handlers de eventos
│   │   └── config/         # Configurações específicas
│   └── presentation/
│       ├── controller/     # Controllers REST
│       └── dto/            # DTOs de apresentação
└── pom.xml
```

### 2. POM.xml do Módulo
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <parent>
        <groupId>com.sakai</groupId>
        <artifactId>ddd-arch-parent</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    
    <artifactId>seu-modulo</artifactId>
    
    <dependencies>
        <dependency>
            <groupId>com.sakai</groupId>
            <artifactId>common-lib</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
        <dependency>
            <groupId>com.sakai</groupId>
            <artifactId>shared-infrastructure</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
    </dependencies>
</project>
```

### 3. Adicione o Módulo ao Parent POM
```xml
<modules>
    <module>common</module>
    <module>infrastructure</module>
    <module>seu-modulo</module>
</modules>
```

## 🎯 Padrões e Convenções

### Domain Layer
```java
// Entidade
@Entity
public class Usuario extends AggregateRoot<UsuarioId> {
    // implementação
}

// Value Object
public class Email extends BaseValueObject {
    // implementação
}

// Evento de Domínio
public class UsuarioCriadoEvent implements DomainEvent {
    // implementação
}
```

### Application Layer
```java
@Service
@Transactional
public class CriarUsuarioService {
    
    @Autowired
    private UsuarioRepository repository;
    
    @Autowired
    private SpringDomainEventPublisher eventPublisher;
    
    public UsuarioId criar(CriarUsuarioCommand command) {
        // lógica de aplicação
        eventPublisher.publish(usuario);
        return usuario.getId();
    }
}
```

### Infrastructure Layer
```java
@Repository
public class JpaUsuarioRepository implements UsuarioRepository {
    // implementação JPA
}

@EventListener
public class UsuarioCriadoHandler {
    @Async
    public void handle(UsuarioCriadoEvent event) {
        // processamento do evento
    }
}
```

## 🔧 Tecnologias

- **Java 17**
- **Spring Boot 3.5.7**
- **Spring Data JPA**
- **Spring Security**
- **H2 Database** (desenvolvimento)
- **Maven**
- **Lombok**
- **ModelMapper**

## 📚 Conceitos DDD Implementados

- ✅ **Entities & Aggregates**
- ✅ **Value Objects**
- ✅ **Domain Events**
- ✅ **Repositories**
- ✅ **Domain Services**
- ✅ **Application Services**
- ✅ **Bounded Contexts** (módulos)
- ✅ **Multi-tenancy Support**

## 🚦 Comandos Úteis

```bash
# Build completo
mvn clean install

# Executar aplicação
mvn spring-boot:run

# Executar testes
mvn test

# Atualizar submódulos
git submodule update --remote

# Adicionar novo submódulo
git submodule add <url> <path>
```

## 📖 Documentação Adicional

- [Common Library](./common/README.md)
- [Infrastructure](./infrastructure/README.md)

## 🤝 Contribuição

1. Fork o projeto
2. Crie uma branch para sua feature
3. Commit suas mudanças
4. Push para a branch
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.