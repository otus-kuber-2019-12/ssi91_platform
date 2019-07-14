FROM nginx:latest

COPY homework.html /app/
COPY nginx.conf /etc/nginx/nginx.conf

RUN useradd -r -u 1001 nginxuser
RUN chown -R nginxuser:nginxuser /app/
RUN touch /var/run/nginx.pid && chown -R 1001 /var/run/nginx.pid
RUN chown -R 1001 /var/cache/nginx/

USER nginxuser

EXPOSE 8000
