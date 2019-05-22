FROM alpine:3.7

# add files
ADD . /var/www

# build
RUN set -x \
    && apk add --update nginx hugo \
    && cd /var/www \
    && hugo \
    && apk del hugo \
    && cp /var/www/nginx.conf /etc/nginx/conf.d/default.conf \
    && mkdir -p /run/nginx

EXPOSE 80

ENTRYPOINT nginx -g 'daemon off;'
