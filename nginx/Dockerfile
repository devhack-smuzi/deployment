FROM nginx
RUN rm /etc/nginx/conf.d/default.conf
COPY ./nginx.conf /etc/nginx/conf.d/default.template

# так длинно, чтоб подставить переменные окружения в конфиг во время запуска
# чтоб не писать все переменные окружения на этап билда
CMD ["/bin/bash", "-c", "envsubst < /etc/nginx/conf.d/default.template > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'"]
