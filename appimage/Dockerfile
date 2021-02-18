FROM appimagecrafters/appimage-builder:0.8.4

WORKDIR /usr/src/app

COPY appimage/AppImageBuilder.yml ./
COPY appimage/ ./appimage

# Add axolotl binary
COPY axolotl ./

# Add axolotl-web bundle
COPY axolotl-web/dist ./axolotl-web/dist

RUN appimage-builder --log INFO
