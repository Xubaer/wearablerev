FROM node:20-alpine

# Install pnpm
RUN corepack enable && corepack prepare pnpm@10.22.0 --activate

# Set working directory
WORKDIR /app

# Copy package files
COPY package.json pnpm-lock.yaml* ./

# Install dependencies
RUN pnpm install --frozen-lockfile || pnpm install

# Copy application files
COPY . .

# Build Strapi admin
RUN pnpm build

# Expose port
EXPOSE 1337

# Start Strapi
CMD ["pnpm", "develop"]
