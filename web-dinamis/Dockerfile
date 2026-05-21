# 1. Builder

FROM node:24-alpine AS builder

# Set Directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json .

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Build Next.js 
RUN npm run build

# 2. Runner
FROM node:24-alpine AS runner

# Set Directory
WORKDIR /app

# Environment variables for Next.js
ENV NODE_ENV=production


# Copy the built files from the builder stage
COPY --from=builder /app/.next/standalone ./.next/standalone/ 
COPY --from=builder /app/.next/static ./.next/static
COPY --from=builder /app/public ./public

#expose port 3000
EXPOSE 3000

# start next.js
CMD ["node", ".next/standalone/server.js"]