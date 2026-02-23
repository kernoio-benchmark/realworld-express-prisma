# Use Node.js LTS version (Debian-based for better Prisma compatibility)
FROM node:18

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./
COPY prisma ./prisma/

# Install all dependencies (including dev dependencies needed for build)
RUN npm ci

# Copy application source
COPY . .

# Generate Prisma client
RUN npx prisma generate

# Build TypeScript application (bypass dotenv requirement)
RUN npx tsc

# Expose port
EXPOSE 3000

# Set environment variables (defaults, can be overridden)
ENV NODE_ENV=production
ENV PORT=3000

# Run database migrations and start the application
CMD npx prisma migrate deploy && npm run start
