# Módulo de Transações - Sistema Financeiro Jala University

## Descrição do Projeto

O **Módulo de Transações** é um componente essencial de um sistema financeiro maior, desenvolvido para gerenciar operações de transferência, beneficiários e histórico de transações. A aplicação utiliza uma arquitetura moderna baseada em **Spring Boot** para o *backend* e **JavaFX** para a interface gráfica de usuário (*frontend*), seguindo o padrão de projeto *Clean Architecture* (ou Arquitetura Hexagonal) para garantir a separação de preocupações, testabilidade e manutenibilidade.

Este módulo permite aos usuários:
*   Realizar transferências bancárias com validação de segurança.
*   Gerenciar uma lista de beneficiários favoritos.
*   Visualizar o histórico detalhado de todas as transações.
*   Acessar funcionalidades de autenticação (Login e Registro).

## Arquitetura e Estrutura de Pastas

O projeto segue uma estrutura de pastas organizada, refletindo a separação de camadas da *Clean Architecture* (Domínio, Aplicação, Infraestrutura e Apresentação), e utiliza o Maven para gerenciamento de dependências.

```
transaction-module-project/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── org/
│   │   │       └── jala/
│   │   │           └── university/
│   │   │               ├── application/                  # Camada de Aplicação (Serviços e Casos de Uso)
│   │   │               │   ├── service/                  # Implementação da lógica de negócio
│   │   │               │   │   ├── BeneficiaryService.java
│   │   │               │   │   └── TransactionServiceImpl.java
│   │   │               │   └── port/                     # Interfaces de entrada e saída (Ports)
│   │   │               │       ├── input/                # Interfaces de entrada (ex: TransactionServicePort)
│   │   │               │       └── output/               # Interfaces de saída (ex: TransactionRepositoryPort)
│   │   │               ├── domain/                       # Camada de Domínio (Regras de Negócio e Entidades)
│   │   │               │   ├── entity/                   # Classes de Entidade (ex: Transaction, User, Beneficiary)
│   │   │               │   ├── exception/                # Exceções de Domínio
│   │   │               │   └── repository/               # Interfaces de Repositório (Contratos)
│   │   │               ├── infrastructure/               # Camada de Infraestrutura (Implementações externas)
│   │   │               │   ├── adapters/                 # Adapters para interfaces de saída
│   │   │               │   └── persistance/              # Implementações de Repositório (JPA)
│   │   │               ├── presentation/                 # Camada de Apresentação (JavaFX Views e Controllers)
│   │   │               │   ├── controller/               # Controladores FXML
│   │   │               │   └── MainView.java             # Classe principal do JavaFX
│   │   │               └── TransactionModuleApplication.java # Classe principal do Spring Boot
│   │   └── resources/
│   │       ├── application.properties              # Configurações do Spring Boot e Banco de Dados
│   │       ├── css/                              # Arquivos de estilo CSS
│   │       ├── icons/                            # Ícones e imagens da aplicação
│   │       └── views/                            # Arquivos FXML para as interfaces de usuário
├── src/
│   └── test/                                     # Testes unitários e de integração
├── pom.xml                                       # Arquivo de configuração do Maven
└── README.md                                     # Este arquivo
```

## Tecnologias Utilizadas

Este projeto combina tecnologias robustas para oferecer uma solução completa e escalável:

| Categoria | Tecnologia | Versão Principal | Propósito |
| :--- | :--- | :--- | :--- |
| **Backend** | Spring Boot | 3.2.4 | Framework para o núcleo da aplicação e injeção de dependência. |
| **Frontend** | JavaFX | 22 | Framework para a construção da interface gráfica de usuário (GUI). |
| **Persistência** | Spring Data JPA | 3.2.4 | Abstração para acesso a dados. |
| **Banco de Dados** | MySQL Connector/J | 8.3.0 | Driver de conexão com o banco de dados MySQL. |
| **Build** | Maven | - | Gerenciamento de projetos e dependências. |
| **Outros** | Lombok | 1.18.30 | Redução de código *boilerplate* (getters, setters, construtores). |
| **Relatórios** | iTextPDF | 5.5.13.4 | Geração de recibos e relatórios em formato PDF. |

## Como Executar o Projeto

Para executar o Módulo de Transações, você precisará configurar o ambiente de desenvolvimento e o banco de dados.

### Pré-requisitos

1.  **Java Development Kit (JDK) 17 ou superior**: Necessário para compilar e executar o código.
2.  **Maven**: Para gerenciar as dependências do projeto.
3.  **Banco de Dados MySQL**: O projeto utiliza JPA e MySQL para persistência de dados. Certifique-se de ter uma instância do MySQL rodando e as credenciais configuradas.
4.  **IntelliJ IDEA** (Recomendado): Ambiente de Desenvolvimento Integrado (IDE) para Java e Spring Boot.

### Configuração do Banco de Dados

1.  Crie um banco de dados MySQL (o nome pode ser configurado).
2.  Edite o arquivo `src/main/resources/application.properties` e configure as propriedades de conexão com o seu banco de dados:

    ```properties
    # Exemplo de configuração no application.properties
    spring.datasource.url=jdbc:mysql://localhost:3306/seu_banco_de_dados?createDatabaseIfNotExist=true
    spring.datasource.username=seu_usuario
    spring.datasource.password=sua_senha
    spring.jpa.hibernate.ddl-auto=update
    ```

### Passos para Execução via IntelliJ IDEA

1.  **Abra o Projeto no IntelliJ IDEA**:
    *   Selecione `File` > `Open...` e navegue até o diretório raiz do projeto `transaction-module-project`.
    *   O IntelliJ IDEA deve reconhecer o arquivo `pom.xml` e importar automaticamente as dependências do Maven.

2.  **Execute a Aplicação**:
    *   Localize a classe principal `TransactionModuleApplication.java` dentro de `src/main/java/org/jala/university/`.
    *   Clique com o botão direito do mouse sobre a classe e selecione `Run \'TransactionModuleApplication.main()\'`.

A aplicação iniciará o contexto do Spring Boot e, em seguida, a interface gráfica do JavaFX será exibida.

## Testes e Cobertura

O projeto inclui testes unitários e de integração para garantir a qualidade do código.

### Execução de Testes

Para executar todos os testes do projeto, utilize o comando Maven:

```bash
mvn clean test
```

### Relatório de Cobertura (JaCoCo)

Para gerar um relatório de cobertura de código, o plugin JaCoCo está configurado. Execute:

```bash
mvn clean verify
```

O relatório HTML de cobertura estará disponível em `target/site/jacoco/index.html`.

## Documentação

O projeto utiliza o padrão de documentação **JavaDoc** para todas as classes, métodos e campos relevantes.

Para gerar a documentação HTML do código, utilize o comando Maven:

```bash
mvn javadoc:javadoc
```

A documentação gerada estará disponível na pasta `target/site/apidocs`.
