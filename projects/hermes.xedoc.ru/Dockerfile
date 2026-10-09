FROM node:24-bookworm
ENV DEBIAN_FRONTEND=noninteractive NODE_OPTIONS=--max-old-space-size=4096
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates git python3 python3-venv python3-pip build-essential pkg-config ffmpeg \
    && rm -rf /var/lib/apt/lists/*
COPY . /src
WORKDIR /src
RUN python3 -m venv /opt/venv \
    && /opt/venv/bin/pip install --no-cache-dir -e ".[dev,web,mcp,cron]"
ENV PATH=/opt/venv/bin:$PATH
RUN npm ci
RUN npm --prefix web install && npm --prefix web run build
RUN npm --prefix ui-tui install && npm --prefix ui-tui run build
CMD ["bash"]
