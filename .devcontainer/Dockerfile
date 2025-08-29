# ベースとなるOSイメージ（Ubuntu）
FROM ubuntu:22.04

# 環境変数の設定
ENV FLUTTER_HOME="/usr/local/flutter"
ENV ANDROID_SDK_ROOT="/usr/local/android-sdk"
ENV PATH="$FLUTTER_HOME/bin:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$ANDROID_SDK_ROOT/platform-tools:$PATH"

# 必要なパッケージのインストールとセットアップ
RUN apt-get update && \
    apt-get install -y curl git unzip wget openjdk-17-jdk && \
    # Flutter SDKのインストール
    git clone https://github.com/flutter/flutter.git -b stable $FLUTTER_HOME && \
    # Android SDK コマンドラインツールのインストール
    mkdir -p $ANDROID_SDK_ROOT && \
    cd $ANDROID_SDK_ROOT && \
    wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip -O cmdline-tools.zip && \
    unzip cmdline-tools.zip && \
    mv cmdline-tools cmdline-tools-temp && \
    mkdir -p $ANDROID_SDK_ROOT/cmdline-tools/latest && \
    mv cmdline-tools-temp/* $ANDROID_SDK_ROOT/cmdline-tools/latest && \
    rm cmdline-tools.zip && \
    # Androidライセンスの同意
    yes | sdkmanager --licenses && \
    # 必要なSDKパッケージのインストール
    sdkmanager "platform-tools" "platforms;android-34" "build-tools;34.0.0" && \
    # Flutter Doctorを実行して事前準備
    flutter doctor

# 作業ディレクトリの設定
WORKDIR /workspace

# デフォルトのコマンド
CMD ["/bin/bash"]