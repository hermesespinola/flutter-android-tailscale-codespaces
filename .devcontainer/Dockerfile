FROM dart

RUN apt-get update
RUN apt-get install -y curl git unzip xz-utils libgconf-2-4 gdb libstdc++6 lib32stdc++6 zip libglu1-mesa sdkmanager

RUN apt-get clean

# Install flutter
RUN git clone https://github.com/flutter/flutter.git -b stable --depth 1 /usr/local/flutter
ENV PATH="/usr/local/flutter/bin:$PATH"

# Enable flutter android
ENV ANDROID_SDK_ROOT=/usr/lib/android-sdk/
RUN sdkmanager --sdk_root "$ANDROID_SDK_ROOT" # && rm -rf $ANDROID_SDK_ROOT/platform-tools # Remove this so the newest version is reinstalled by sdkmanager
RUN sdkmanager --install "platform-tools;35.0.2" "cmdline-tools;latest" "build-tools;35.0.0" "cmake;3.22.1" "ndk;r27" "platforms;android-35"
ENV PATH="$ANDROID_SDK_ROOT/platform-tools:$PATH"
RUN flutter config --android-sdk "$ANDROID_SDK_ROOT" && flutter config --enable-android
RUN yes | flutter doctor --android-licenses
