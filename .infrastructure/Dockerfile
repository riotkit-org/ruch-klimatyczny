FROM alpine:3.9

# add files
ADD . /var/www

# build
RUN set -x \
    && apk add --update nginx \
    && sed -i 's/v3\.9/edge/g' /etc/apk/repositories \
    && apk add --update hugo \
    \
    && cd /var/www \
    && hugo -v \
    && apk del hugo \
    \
    && cp /var/www/.infrastructure/nginx.conf /etc/nginx/conf.d/default.conf \
    && mkdir -p /run/nginx \
    \
    && mv /var/www /var/www.tmp \
    && mkdir -p /var/www \
    && mv /var/www.tmp/public /var/www/public \
    && rm -rf /var/www.tmp

EXPOSE 80

ENTRYPOINT nginx -g 'daemon off;'
