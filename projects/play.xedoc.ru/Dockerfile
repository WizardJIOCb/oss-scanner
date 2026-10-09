FROM node:24-bookworm
ENV DEBIAN_FRONTEND=noninteractive NODE_OPTIONS=--max-old-space-size=4096
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates git python3 python3-venv python3-pip build-essential pkg-config ffmpeg \
    && rm -rf /var/lib/apt/lists/*
COPY . /src
WORKDIR /src
RUN npm ci
RUN npm run build
RUN python3 -m venv /opt/venv && /opt/venv/bin/pip install --no-cache-dir -r backend/requirements-dev.txt
ENV PATH=/opt/venv/bin:$PATH
CMD ["bash"]
