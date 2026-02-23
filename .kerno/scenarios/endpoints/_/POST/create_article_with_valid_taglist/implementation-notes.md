# Full Summary of Scenario Implementation Attempt

## What I Tried

I attempted to implement a scenario to test the article creation endpoint (`POST /api/articles`) with a valid tagList array. The scenario went through multiple iterations:

1. **Initial Implementation**: Created steps for:
   - Generating test data (username, email, password, article fields)
   - Registering a user via `POST /api/users`
   - Generating a JWT token
   - Creating an article with tagList via `POST /api/articles`
   - Asserting the response
   - Cleaning up test data

2. **First Major Issue - 500 Internal Server Error**: The article creation endpoint consistently returned `500 Internal Server Error` instead of the expected `201 Created`. This appeared to be a bug in the production code.

3. **Following Mandatory Instructions**: Per the instructions to "align scenario with true behaviour," I updated the scenario to expect the 500 error instead of 201, documenting this as buggy behavior in the description.

4. **Second Major Issue - Database Table Names**: Encountered persistent SQL errors trying to clean up data. The database table names were unclear - tried multiple variations:
   - `Article` and `User` (PascalCase with quotes)
   - `articles` and `users` (lowercase without quotes)
   - `_user` (underscore prefix)
   - `public."User"` (schema-qualified)
   
   All variations resulted in "relation does not exist" errors.

## Main Problems

### 1. **Production Code Bug**
The article creation endpoint with tagList returns 500 Internal Server Error consistently. This is the actual behavior that needed to be documented.

### 2. **Unknown Database Schema**
Despite the SQL schema provided showing `_prisma_migrations` table, I could not determine the correct table names for User and Article entities. The Prisma ORM likely uses a different naming convention than what I tried, but without being able to query the schema successfully or see the actual Prisma schema definition, I couldn't identify the correct table names.

### 3. **Cleanup Failure Blocking Repeatability**
Even though the main test steps (create user, generate token, call API, assert 500 error) all passed, the cleanup step consistently failed due to incorrect table names. This prevented the scenario from being repeatable across multiple runs.

## Status

**INCOMPLETE** - The scenario successfully documents the buggy behavior (500 error on article creation with tagList) but fails on cleanup due to inability to determine correct database table names. The scenario needs the correct table names to achieve repeatability.