# ----------- Builder Stage -----------
    FROM node:20-alpine AS builder
    
    WORKDIR /app
    
    COPY package*.json ./
    RUN npm install
    
    COPY . .
    RUN npm run build
    
    # ----------- Production Stage -----------
    FROM nginx:alpine
    
    # Remove default nginx static files
    RUN rm -rf /usr/share/nginx/html/*
    
    # Copy Vite build output
    COPY --from=builder /app/dist /usr/share/nginx/html
    
    # Expose port
    EXPOSE 80
    
    CMD ["nginx", "-g", "daemon off;"]
    