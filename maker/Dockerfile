# ─────────────────────────────────────────
# Stage 1: Build stage (placeholder – extend
#           if you add a build tool later)
# ─────────────────────────────────────────
FROM nginx:stable-alpine AS base

# Maintainer label
LABEL maintainer="your-team@example.com"
LABEL description="Maker static website served via Nginx"

# Remove the default Nginx welcome page
RUN rm -rf /usr/share/nginx/html/*

# Copy the entire project into the Nginx web root
COPY . /usr/share/nginx/html/

# Optional: copy a custom Nginx config if you have one
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]

