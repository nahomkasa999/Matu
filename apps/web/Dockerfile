# Stage 1: Build the Next.js application
FROM node:20-alpine AS builder

WORKDIR /app/apps/web

# Copy monorepo root package.json and pnpm-lock.yaml
COPY package.json pnpm-lock.yaml ./
COPY turbo.json ./
COPY apps/web/package.json apps/web/
COPY packages/ packages/

# Install dependencies for the entire monorepo
RUN pnpm install --frozen-lockfile

# Build the Next.js application
RUN pnpm --filter=web build

# Stage 2: Run the Next.js application
FROM node:20-alpine AS runner

WORKDIR /app/apps/web

# Set environment variables for Next.js
ENV NODE_ENV production

# Copy necessary files from the builder stage
COPY --from=builder /app/apps/web/.next/standalone ./
COPY --from=builder /app/apps/web/.next/static ./.next/static
COPY --from=builder /app/apps/web/public ./public

# Expose the port Next.js listens on
EXPOSE 3000

# Define the command to run the Next.js application
CMD ["pnpm", "run", "dev"]