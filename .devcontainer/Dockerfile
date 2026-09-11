FROM debian:trixie

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates curl git zsh tmux openssh-client sudo atuin starship bat \
    zsh-autosuggestions zsh-syntax-highlighting \
    nodejs npm ncurses-term \
    iptables iproute2 jq \
    && rm -rf /var/lib/apt/lists/*

# Tailscale client
RUN curl -fsSL https://pkgs.tailscale.com/stable/debian/trixie.noarmor.gpg \
      -o /usr/share/keyrings/tailscale-archive-keyring.gpg \
 && curl -fsSL https://pkgs.tailscale.com/stable/debian/trixie.tailscale-keyring.list \
      -o /etc/apt/sources.list.d/tailscale.list \
 && apt-get update && apt-get install -y --no-install-recommends tailscale \
 && rm -rf /var/lib/apt/lists/*

ARG USERNAME=dev
RUN useradd -m -s /bin/bash $USERNAME \
    && echo "$USERNAME ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/$USERNAME
