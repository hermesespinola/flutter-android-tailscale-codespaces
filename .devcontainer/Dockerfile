FROM dart

RUN apt-get update
RUN apt-get install -y curl git gh unzip xz-utils zip libglu1-mesa android-sdk android-tools android-sdk-platform-tools sdkmanager

RUN apt-get clean

ENV ANDROID_SDK_ROOT=/usr/lib/android-sdk/

RUN sdkmanager --sdk_root "$ANDROID_SDK_ROOT"
RUN sdkmanager --install "build-tools;35.0.0" "cmake;3.22.1" "ndk;r27" "platforms;android-35" "platform-tools;35.0.2"

RUN git clone https://github.com/flutter/flutter.git -b stable --depth 1 /flutter
ENV PATH="$ANDROID_SDK_ROOT/platform-tools:/flutter/bin:$PATH"

RUN flutter config --android-sdk "$ANDROID_SDK_ROOT" && flutter config --enable-android
RUN yes | sdkmanager --licenses && yes | flutter doctor --android-licenses && flutter doctor
