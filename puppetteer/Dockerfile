FROM alpine:3.10.3

# Installs latest Chromium (77) package.
RUN apk add --no-cache --update \
  chromium=~77 \
  nss=~3 \
  freetype=~2 \
  freetype-dev=~2 \
  harfbuzz=~2 \
  ca-certificates=~20190108 \
  ttf-freefont=~20120503 \
  nodejs=~10 \
  yarn=~1

# Tell Puppeteer to skip installing Chrome. We'll be using the installed package.
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD true

# Add user so we don't need --no-sandbox.
RUN addgroup -S pptruser && adduser -S -g pptruser pptruser \
    && mkdir -p /home/pptruser/Downloads /app \
    && chown -R pptruser:pptruser /home/pptruser \
    && chown -R pptruser:pptruser /app

# Run everything after as non-privileged user.
USER pptruser
