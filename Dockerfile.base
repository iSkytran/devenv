FROM ubuntu:22.04
SHELL ["/bin/bash", "-c"]

# Arguments
ARG USERNAME=entran
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Add non-root user.
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME
USER $USERNAME

# Install basic utilities.
RUN sudo apt-get update \
    && sudo apt-get install build-essential curl git vim zsh -y

# Install oh-my-zsh.
RUN ZSH="/usr/share/oh-my-zsh" sudo sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" --unattended \
    && sudo git clone https://github.com/zsh-users/zsh-autosuggestions.git /usr/share/oh-my-zsh/plugins/zsh-autosuggestions \
    && sudo git clone https://github.com/zsh-users/zsh-syntax-highlighting.git /usr/share/oh-my-zsh/plugins/zsh-syntax-highlighting \
    && sudo git clone https://github.com/sindresorhus/pure.git /usr/share/oh-my-zsh/pure \
    && sudo cp /usr/share/oh-my-zsh/pure/pure.zsh /usr/share/zsh/functions/Prompts/prompt_pure_setup \
    && sudo cp /usr/share/oh-my-zsh/pure/async.zsh /usr/share/zsh/functions/Prompts/async

# Install dotfiles.
RUN git clone --bare https://github.com/iSkytran/dotfiles.git $HOME/.dotfiles \
    && git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME checkout --force

WORKDIR /home/$USERNAME
CMD ["/bin/zsh"]
