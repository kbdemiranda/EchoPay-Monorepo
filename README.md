# EchoPay Monorepo

The EchoPay Monorepo consolidates the **EchoPay** and **EchoPay-Processor** services into one repository for streamlined development and deployment of the complete financial transaction processing system. This setup allows easy coordination between the EchoPay API and the processing microservice, which communicate via Kafka and store transaction data in PostgreSQL.

## Requirements

- **Java 21** (Amazon Corretto)
- **Maven 3.8+**
- **Docker** and **Docker Compose**
- **Kafka**
- **PostgreSQL**

## Setup and Execution

### 1. Clone the repository

```bash
git clone https://github.com/your-username/EchoPay-Monorepo.git
cd EchoPay-Monorepo
```

### 2. Configure Docker Compose

The project includes a `docker-compose.yml` file to run the required services:
- **EchoPay**: Handles transaction requests via REST API.
- **EchoPay-Processor**: Processes transactions and updates their status.
- **PostgreSQL**: Stores transaction data.
- **Kafka and Zookeeper**: Message broker to facilitate communication between services.

Run the following command to start all containers:

```bash
docker-compose up
```

### 3. Access Swagger

Once the containers are running, the Swagger UI for EchoPay is available for testing API endpoints:

```bash
http://localhost:8080/swagger-ui.html
```

### 4. Main Endpoints

- **EchoPay API**:
  - `POST /api/transactions` - Create a new transaction.
  - `GET /api/transactions/{uuid}` - Retrieve a transaction by UUID.
  - `PUT /api/transactions/{uuid}/status` - Update the status of a transaction.

## Environment Variables

Key environment variables configured in `docker-compose.yml`:

- `SPRING_DATASOURCE_URL`: URL for the PostgreSQL database connection.
- `SPRING_KAFKA_BOOTSTRAP_SERVERS`: Configured Kafka server.
- `ECHOPAY_SERVICE_URL`: URL for communicating between EchoPay and EchoPay-Processor.

## Project Structure

```bash
├── echopay/              # Main EchoPay service (API)
│   ├── application/      # Controllers, DTOs, and services
│   ├── domain/           # Domain models and enums
│   └── infrastructure/   # Database, Kafka configurations, and exceptions
│
├── echopay-processor/    # EchoPay-Processor service
│   ├── application/      # Services for transaction processing
│   └── infrastructure/   # Kafka configurations
│
├── docker-compose.yml    # File to orchestrate the containers
└── Dockerfiles/          # Docker configuration files for both services
```

## Technologies Used

- **Spring Boot**: Framework for building and managing the services.
- **Kafka**: For messaging between EchoPay and EchoPay-Processor.
- **PostgreSQL**: Relational database for storing transactions.
- **Docker**: Containerization for easy deployment.

## Author

Developed by **Kaique de Miranda**.
