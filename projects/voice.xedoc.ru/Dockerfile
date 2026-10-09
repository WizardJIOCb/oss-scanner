FROM node:24-bookworm
ENV DEBIAN_FRONTEND=noninteractive NODE_OPTIONS=--max-old-space-size=4096
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates git python3 python3-venv python3-pip build-essential pkg-config ffmpeg \
    && rm -rf /var/lib/apt/lists/*
COPY . /src
WORKDIR /src
RUN python3 -m venv /opt/server-venv \
    && /opt/server-venv/bin/pip install --no-cache-dir -r server/requirements.txt pytest httpx
RUN /opt/server-venv/bin/python -m compileall -q server/app worker
ENV PATH=/opt/server-venv/bin:$PATH
CMD ["bash"]
