# Blogging Website - Medium Clone

## The TechStack Used -
1. React in the frontend
2. Cloudflare workers in the backend
3. zod as the validation library, type inference for the frontend types
4. Typescript as the language
5. Prisma as the ORM, with connection pooling
6. Postgres as the database
7. jwt for authentication

## Step 1- Creating Backend
* create a main folder and inside we create another floder with name backend using command - npm create hono@latest

## Step 2 - Initialize handlers
* To begin with, our backend will have 4 routes
1. POST /api/v1/user/signup
2. POST /api/v1/user/signin
3. POST /api/v1/blog
3. PUT /api/v1/blog
4. GET /api/v1/blog/:id
5. GET /api/v1/blog/bulk

## Step 3 - Initialize DB (prisma)
* It is one of the crucial part of the appication because we try to use prisma in serverless backend.
1. Get your connection url from neon.db or aieven.tech

2. Get connection pool URL from Prisma accelerate
https://www.prisma.io/data-platform/accelerate

3. Initialize prisma in project
* Make sure we in the backend folder
```.js
npm i prisma
npx prisma init
```
* Replace DATABASE_URL in .env
DATABASE_URL="postgres://avnadmin:password@host/db"

* Add DATABASE_URL as the connection pool url in wrangler.toml

4. Initialize the schema

5. Migrate Database
npx prisma migrate dev --name init_schema

6. Generate the prisma client
npx prisma generate --no-engine

7. Add the accelerate extension
npm install @prisma/extension-accelerate

8. Initialize the prisma client
```.js
import { PrismaClient } from '@prisma/client/edge'
import { withAccelerate } from '@prisma/extension-accelerate'
const prisma = new PrismaClient({
 datasourceUrl: env.DATABASE_URL,
}).$extends(withAccelerate())
```

## Step 4 - Create non auth routes
4.1 - Add JWT to signup route </br>
4.2 - Add a signin route 