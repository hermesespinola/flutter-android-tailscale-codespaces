FROM dart

RUN apt-get update
RUN apt-get install -y curl git unzip xz-utils libgconf-2-4 gdb libstdc++6 lib32stdc++6 zip libglu1-mesa android-sdk sdkmanager

RUN apt-get clean

# Install flutter
RUN git clone https://github.com/flutter/flutter.git -b stable --depth 1 /usr/local/flutter
ENV PATH="/usr/local/flutter/bin:$PATH"
RUN flutter doctor

# Enable flutter android
ENV ANDROID_SDK_ROOT=/usr/lib/android-sdk/
RUN sdkmanager --sdk_root "$ANDROID_SDK_ROOT"
RUN sdkmanager --install "platform-tools;latest" "cmdline-tools;latest" "build-tools;latest" "cmake;latest" "ndk;latest" "platforms;latest"
ENV PATH="$ANDROID_SDK_ROOT/platform-tools:$PATH"
RUN flutter config --android-sdk "$ANDROID_SDK_ROOT" && flutter config --enable-android
RUN yes | flutter doctor --android-licenses
