# Use the official Nginx image from the Docker Hub
FROM nginx:alpine

# Expose port 80
EXPOSE 80

# Copy custom Nginx config file
COPY nginx-default.conf /etc/nginx/conf.d/default.conf

# Start Nginx when the container has started
CMD ["nginx", "-g", "daemon off;"]
