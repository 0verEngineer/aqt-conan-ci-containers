FROM stateoftheartio/qt6:6.8-gcc-aqt

USER root

# Set env variables
ENV QT_VERSION=6.8.0

# Install deps
RUN apt update -y
RUN apt install -y python3 python3-pip wget desktop-file-utils libgl-dev libvulkan-dev fuse libfuse2 file lcov bc xmlstarlet

RUN pip install --no-cache-dir conan junitparser lcov_cobertura

# linuxdeploy-plugin-appimage
RUN git clone https://github.com/linuxdeploy/linuxdeploy-plugin-appimage /tmp/lpa/
RUN git -C /tmp/lpa/linuxdeploy-plugin-appimage checkout c529d31fbce034875f0829c3bd7c66d5531c88d1
RUN git -C /tmp/lpa/linuxdeploy-plugin-appimage submodule update --init --recursive
RUN cmake /tmp/lpa/linuxdeploy-plugin-appimage -B /tmp/lpa/linuxdeploy-plugin-appimage-build -G Ninja -DCMAKE_INSTALL_PREFIX=/usr/local -DCMAKE_BUILD_TYPE=Release -DUSE_CCACHE=OFF
RUN cmake --build /tmp/lpa/linuxdeploy-plugin-appimage-build
RUN mv /tmp/lpa/linuxdeploy-plugin-appimage-build/src/linuxdeploy-plugin-appimage /usr/local/bin/

# download appimage tool (requires fuse and file)
RUN mkdir /tmp/appimagetool
RUN cd /tmp/appimagetool
RUN wget "https://github.com/AppImage/AppImageKit/releases/download/continuous/appimagetool-x86_64.AppImage"
RUN chmod a+x appimagetool-x86_64.AppImage
RUN mv appimagetool-x86_64.AppImage /usr/local/bin/

RUN apt autoremove && apt clean
RUN rm -r /tmp/*

USER user
