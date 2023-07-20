---
layout: post
title: "サンプル Spring アプリ を用意、実行するコマンド"
date: 2023-04-02 00:00:00
tags: [java]
---

java 1.17 を入れる手順も含むので空のVM 等で実施する事をお勧めします。

# 環境
ubuntu 20.04 on WSL で確認

# コマンド
```
wget https://aka.ms/download-jdk/microsoft-jdk-17-linux-x64.tar.gz
tar -zxf microsoft-jdk-17*.tar.gz
cd jdk-17*
export JAVA_HOME=`pwd`
cd ..
export PATH=${JAVA_HOME}/bin:$PATH
java -version
mkdir SpringBoot
git clone https://github.com/spring-guides/gs-spring-boot-for-azure
cd gs-spring-boot-for-azure/complete
./mvnw clean package #Failed するかもしれませんが無視して起動できました。
./mvnw spring-boot:run
```

# java-optsを指定する場合
環境変数 MAVEN_OPTS をいじります。

```
export MAVEN_OPTS="-javaagent:/root/SpringBoot/gs-spring-boot-for-azure/complete/applicationinsights-agent-3.4.13.jar";./mvnw spring-boot:run
```

# 参考
https://spring.pleiades.io/guides/gs/spring-boot-for-azure/
