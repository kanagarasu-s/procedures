# Stage 1 — Build the Vite frontend
FROM node:22-slim AS build

# Set working directory
WORKDIR /app

# Install pnpm globally
RUN npm install -g pnpm

# Copy dependency files first (for better layer caching)
COPY package.json pnpm-lock.yaml* ./

# Install dependencies
RUN pnpm install

# Copy all source code
COPY . .

# Build production-ready files
RUN pnpm run build

# Stage 2 — Serve with Apache2

FROM httpd:2.4 AS production

# Remove default Apache HTML files
RUN rm -rf /usr/local/apache2/htdocs/*

# Copy built app from the previous stage
COPY --from=build /app/dist/ /usr/local/apache2/htdocs/

# Optional: custom Apache configuration (for React Router)
COPY apache.conf /usr/local/apache2/conf/httpd.conf

# Expose port 80
EXPOSE 80

# Start Apache in foreground
CMD ["httpd-foreground"]
