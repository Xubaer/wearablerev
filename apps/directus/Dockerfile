FROM node:20-alpine

# Install pnpm
RUN corepack enable && corepack prepare pnpm@10.22.0 --activate

# Set working directory
WORKDIR /directus

# Copy package files
COPY package.json pnpm-lock.yaml* ./

# Install dependencies
RUN pnpm install --frozen-lockfile || pnpm install

# Copy application files (if any custom extensions)
COPY . .

# Create necessary directories
RUN mkdir -p uploads extensions

# Expose port
EXPOSE 8055

# Start Directus
CMD ["pnpm", "start"]
