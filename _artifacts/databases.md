---
title: "Databases"
collection: artifacts
type: "Undergraduate course"
permalink: /artifacts/databases
excerpt: ""
---
| Artifact                         | GitHub Link | Download Link |
|----------------------------------|------------|---------------|
| Initial Artifact (Before Enhancements) | [View on GitHub](https://github.com/phillipkangsnhu/CS-499/tree/5576f6853deb3191535deefb915f2dd415426cde) | [Download ZIP](https://github.com/phillipkangsnhu/CS-499/archive/5576f6853deb3191535deefb915f2dd415426cde.zip) |
| Enhanced Artifact | [View on GitHub](https://github.com/phillipkangsnhu/CS-499) | [Download ZIP](https://github.com/phillipkangsnhu/CS-499/archive/refs/heads/main.zip) | 
| Narrative | N/A | [Download File]({{base_path}}/files/DatabasesNarrativePhillipKang.docx) |

This artifact is the database portion of my CS-465 Full Stack Development I final project. It was a mongoDB database that used a JSON file to initialize, and had an ORM layer to allow the application to interact with the data. 

I included this artifact in my ePortfolio because, along with the enhancement, it showcases my knowledge of both NoSQL and SQL databases. Specifically, changing the database from mongoDB to a SQL database and updating the ORM layer so that it can use this SQL database shows my understanding of how the two kinds of databases are similar and different. 

Through this enhancement, I demonstrate my analysis of databases and my thought process behind design choices between NoSQL and SQL. Weighing between the trade-offs and understanding what is required within this project also show my skills in implementing well-founded solutions to accomplish the goals of this enhancement.

Through the process of enhancing this artifact, I found that updating the database also tied in with my other enhancement of containerizing parts of the application. Because I wanted to isolate this specific part of the enhancement to only Databases, I opted to use sqlite3 as the SQL database.


## Course Outcomes Examples
### CS-499-01: Collaborative Environment
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`docker-compose.yaml`](https://github.com/phillipkangsnhu/CS-499/blob/main/docker-compose.yaml#L1-L24)
``` yaml
version: '3.8'

services:
  angular:
    build: ./app_admin
    ports:
      - "4200:4200"
    volumes:
      - ./app_admin:/app
      - /app/node_modules
    env_file:
      - .env
    command: npm run start

  api:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/app
      - /app/node_modules
    env_file:
      - .env
    command: npm run start
```
[`.seedgoosers.js`](https://github.com/phillipkangsnhu/CS-499/blob/main/.seedgooserc.js#L1-L11)
``` javascript
module.exports = {
  modelBaseDirectory: "app_server/database/models", // model directory name
  models: ["*.js", "!db.js"], // model matcher
  data: "data", // data directory name
};
```
</details>  
This enhancement fosters a collaborative development environment by containerizing the database and application services using Docker. By defining services in docker-compose.yaml, team members can quickly spin up identical local development environments without manual setup, reducing inconsistencies across different machines. This ensures seamless integration between front-end and back-end developers and improves productivity by eliminating environment-related issues.

<div style="margin-top: 10px;"></div>
### CS-499-02: Professional Implementation
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`knexfile.js`](https://github.com/phillipkangsnhu/CS-499/blob/main/knexfile.js#L3-L47)
``` javascript
/**
 * @type { Object.<string, import("knex").Knex.Config> }
 */
module.exports = {

  development: {
    client: 'sqlite3',
    connection: {
      filename: './dev.sqlite3'
    }
  },

  staging: {
    client: 'postgresql',
    connection: {
      database: 'my_db',
      user:     'username',
      password: 'password'
    },
    pool: {
      min: 2,
      max: 10
    },
    migrations: {
      tableName: 'knex_migrations'
    }
  },

  production: {
    client: 'postgresql',
    connection: {
      database: 'my_db',
      user:     'username',
      password: 'password'
    },
    pool: {
      min: 2,
      max: 10
    },
    migrations: {
      tableName: 'knex_migrations'
    }
  }

};
```
</details>  
This configuration follows industry best practices by structuring environment-specific database settings in knexfile.js. It ensures that different environments—development, staging, and production—use appropriate database technologies while maintaining consistent migrations and connection pooling strategies. The ability to transition between SQLite (local) and PostgreSQL (production) highlights adaptability and professional-grade database implementation.

<div style="margin-top: 10px;"></div>
### CS-499-03: Trade-off Management
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`knexfile.js`](https://github.com/phillipkangsnhu/CS-499/blob/main/knexfile.js#L8-L45)
``` javascript
  development: {
    client: 'sqlite3',
    connection: {
      filename: './dev.sqlite3'
    }
  },

  staging: {
    client: 'postgresql',
    connection: {
      database: 'my_db',
      user:     'username',
      password: 'password'
    },
    pool: {
      min: 2,
      max: 10
    },
    migrations: {
      tableName: 'knex_migrations'
    }
  },

  production: {
    client: 'postgresql',
    connection: {
      database: 'my_db',
      user:     'username',
      password: 'password'
    },
    pool: {
      min: 2,
      max: 10
    },
    migrations: {
      tableName: 'knex_migrations'
    }
  }
```
</details>  
This enhancement required carefully balancing trade-offs between NoSQL and SQL databases. MongoDB initially provided flexibility and easy scaling, but PostgreSQL was chosen for production due to its strong relational integrity and transactional support. SQLite was selected for local development to maintain portability without requiring a full database server. This decision demonstrates an understanding of database trade-offs, prioritizing scalability, data integrity, and ease of development.

<div style="margin-top: 10px;"></div>
### CS-499-05: Data Security
<details markdown="1" style="margin-top: 5px;margin-bottom:5px;">
<summary>
code snippet (click to expand)
</summary>

[`.seedgoosers.js`](https://github.com/phillipkangsnhu/CS-499/blob/main/.seedgooserc.js#L1-L11)
``` javascript
module.exports = {
  modelBaseDirectory: "app_server/database/models", // model directory name
  models: ["*.js", "!db.js"], // model matcher
  data: "data", // data directory name
};
```
</details>  
Security considerations were integrated into this enhancement by ensuring proper database initialization and avoiding exposure of sensitive information. The database seeding process is controlled to prevent unauthorized data manipulation, and configuration details are managed securely via environment variables instead of hardcoded credentials. Future improvements will include implementing encryption for sensitive fields and enforcing role-based access controls to minimize security risks.
