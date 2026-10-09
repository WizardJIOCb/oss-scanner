FROM golang:1.26-bookworm AS go-runtime
FROM node:24-bookworm
ENV DEBIAN_FRONTEND=noninteractive PATH=/usr/local/go/bin:$PATH
COPY --from=go-runtime /usr/local/go /usr/local/go
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates git python3 python3-venv cmake ninja-build build-essential pkg-config \
    && rm -rf /var/lib/apt/lists/*
COPY . /src
WORKDIR /src
RUN go build -o /src/build-studio ./demo
RUN npm --prefix apps/studio-web ci && npm --prefix apps/studio-web run build
RUN cmake -S /src -B /src/build-cpu -G Ninja -DCMAKE_BUILD_TYPE=RelWithDebInfo -DKIMODO_ENABLE_VULKAN=OFF \
    && cmake --build /src/build-cpu -j2
CMD ["bash"]
