# Gunakan image dasar Nginx
FROM nginx:alpine

# Salin konfigurasi Nginx dan file HTML ke dalam container
COPY ./default.conf /etc/nginx/conf.d/default.conf
COPY ./html /usr/share/nginx/html

# Expose port 80 untuk HTTP
EXPOSE 80
