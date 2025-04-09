FROM stateoftheartio/qt6:6.8-macos-aqt

USER root

# Deps
RUN apt update
RUN apt install -y --no-install-suggests --no-install-recommends python3 python3-pip make

RUN pip install conan

RUN apt autoremove && apt clean

USER user
