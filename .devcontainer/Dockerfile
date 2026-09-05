FROM debian:trixie

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates curl git zsh tmux openssh-client sudo atuin starship bat \
    zsh-autosuggestions zsh-syntax-highlighting \
    nodejs npm ncurses-term \
    && rm -rf /var/lib/apt/lists/*

ARG USERNAME=dev
RUN useradd -m -s /bin/bash $USERNAME \
    && echo "$USERNAME ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/$USERNAME
