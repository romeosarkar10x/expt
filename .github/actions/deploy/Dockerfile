FROM debian:latest

ENV NODE_VERSION="24.0.1"
ENV DART_SASS_VERSION="1.88.0"
ENV HUGO_VERSION="0.147.3"

# Install necessary packages
RUN <<EOF
apt-get update
apt-get install -y git wget xz-utils
EOF

# Install `node` and `npm`
RUN <<EOF
mkdir /node.js
wget https://nodejs.org/download/release/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.xz
tar -xf node-v${NODE_VERSION}-linux-x64.tar.xz -C /node.js --strip-components=1
EOF

# Install `dart-sass`
RUN <<EOF
mkdir /dart-sass
wget https://github.com/sass/dart-sass/releases/download/${DART_SASS_VERSION}/dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz
tar -xzf dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz -C /dart-sass --strip-components=1
rm dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz
EOF

# Install `hugo`
RUN <<EOF
mkdir /hugo
wget https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_linux-amd64.tar.gz
tar -xzf hugo_${HUGO_VERSION}_linux-amd64.tar.gz -C /hugo
rm hugo_${HUGO_VERSION}_linux-amd64.tar.gz
EOF

ENV PATH=/node.js/bin:/dart-sass:/hugo:${PATH}

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]