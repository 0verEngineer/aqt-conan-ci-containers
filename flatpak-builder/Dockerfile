FROM ubuntu:22.04

USER root

# Install deps
RUN apt update -y
RUN apt install -y wget desktop-file-utils libgl-dev libvulkan-dev file flatpak flatpak-builder ccache sudo
#python3-aiohttp python3-tenacity python3-gobject xorg-x11-server-Xvfb zstd

RUN flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
#RUN flatpak remote-add --if-not-exists flathub-beta https://flathub.org/beta-repo/flathub-beta.flatpakrepo
#RUN flatpak remote-add --if-not-exists gnome-nightly https://nightly.gnome.org/gnome-nightly.flatpakrepo

RUN wget https://raw.githubusercontent.com/flatpak/flat-manager/master/flat-manager-client
RUN mv flat-manager-client /usr/local/bin/
RUN chmod +x /usr/local/bin/flat-manager-client

RUN apt autoremove && apt clean

# Add group & user + sudo
RUN groupadd -r user
RUN useradd --create-home --gid user user
RUN echo 'user ALL=NOPASSWD: ALL' > /etc/sudoers.d/user

USER user
WORKDIR /home/user
ENV HOME /home/user
