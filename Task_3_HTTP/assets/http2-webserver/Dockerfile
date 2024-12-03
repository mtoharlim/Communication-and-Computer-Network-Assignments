# Gunakan image dasar Nginx
FROM nginx:alpine

# Salin konfigurasi Nginx dan sertifikat SSL
COPY ./default.conf /etc/nginx/conf.d/default.conf
COPY ./ssl /etc/nginx/ssl
COPY ./html /usr/share/nginx/html

# Expose port 443 untuk HTTPS
EXPOSE 443
