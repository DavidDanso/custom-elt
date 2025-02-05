# Custom ELT Project

A minimal ELT (Extract, Load, Transform) project powered by Docker and PostgreSQL.

---

## Repository Structure

- **docker-compose.yaml**  
  - Orchestrates three containers:
    - **source_postgres**: The source PostgreSQL database.
    - **destination_postgres**: The destination PostgreSQL database.
    - **elt_script**: Runs the ELT process.

- **elt_script/Dockerfile**  
  - Sets up a Python environment.
  - Installs the PostgreSQL client.
  - Copies the ELT script into the container and defines the default command.

- **elt_script/elt_script.py**  
  - Waits for the source database to be ready.
  - Dumps data from the source using `pg_dump`.
  - Loads the dumped data into the destination using `psql`.

- **source_db_init/init.sql**  
  - Initializes the source database.
  - Creates tables for users, films, film categories, actors, and film actors.
  - Inserts sample data into these tables.

---

## How It Works

1. **Container Setup**  
   - Docker Compose starts three containers:
     - A source PostgreSQL database preloaded with sample data.
     - A destination PostgreSQL database.
     - A Python container that executes the ELT script.

2. **ELT Process**  
   - The ELT script waits until the source database is available.
   - It uses `pg_dump` to export the source database to a SQL file.
   - It then imports this SQL file into the destination database using `psql`.

3. **Database Initialization**  
   - The `init.sql` file creates the necessary tables and populates them with sample data in the source database.

---

## Getting Started

1. **Prerequisites**  
   - Install Docker and Docker Compose on your machine.

2. **Setup**  
   - Clone the repository.
   - Navigate to the repository directory.

3. **Run the Project**  
   - Execute the command:
     ```bash
     docker-compose up
     ```
   - The ELT process will start automatically once the containers are up.

4. **Access Databases**  
   - Source PostgreSQL database: Port **5433**
   - Destination PostgreSQL database: Port **5434**
