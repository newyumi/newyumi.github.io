---
layout: post
title:  "electron을 이용해서 웹페이지를 애플리케이션으로 배포하기"
subtitle: "#electron"
type: "Deploy web page using electron"
development: true
text: true
author: "Yumi Yang"
post-header: false
header-img: "electron/img/header.jpg"
order: 1
date: 2018-12-19
comments: true
---


목적은 단지 웹페이지를 앱st 하는 것이기 때문에 electron-quick-start git을 다운받고 페이지 주소를 넣어서 로딩하였다. 별 일은 아니었지만 삽질의 기록을 남긴다.


```
# Clone this repository
git clone https://github.com/electron/electron-quick-start
# Go into the repository
cd electron-quick-start
# Install dependencies
npm install
# Run the app
npm start
```

실행 후 바로 전체화면 적용을 위해 fullscreen: true 옵션과 배경색을 적용.

```javascript
mainWindow = new BrowserWindow({
    width: 1920,
    height: 1080,
    backgroundColor: '#0D0D0D',
    fullscreen: true
});
```

기본적으로 index.html 파일을 적용하는데 이부분을 url로 대체하였다. (예시로 나의 blog 주소를 넣었음)

```javascript
mainWindow.loadFile('index.html');
mainWindow.loadURL('https://newyumi.github.io/');
```

그 후 패키징 툴이 여러개 있는데 electron 문서에서는 3가지를 추천한다.

<br/><br/>

***

<br/><br/>

참고: [https://electronjs.org/docs/tutorial/application-distribution](https://electronjs.org/docs/tutorial/application-distribution)

애플리케이션을 일일이 수동으로 패키지로 만드는 대신, 서드 파티 패키징 툴을 사용하며 이러한 작업을 자동화 시킬 수 있습니다.

* [electron-forge](https://github.com/electron-userland/electron-forge)
* [electron-builder](https://github.com/electron-userland/electron-builder)
* [electron-packager](https://github.com/electron-userland/electron-packager)

이 중에서 간단해 보이는 electron-packager를 사용했다.

<br/>
참고: [https://github.com/electron-userland/electron-packager#building-windows-apps-from-non-windows-platforms](https://github.com/electron-userland/electron-packager#building-windows-apps-from-non-windows-platforms)


```
# For use in npm scripts (recommended)
npm install electron-packager --save-dev

# For use from the CLI
npm install electron-packager -g
```

명령어는 아주 간단하다.

```
electron-packager <sourcedir> <appname> --platform=<platform> --arch=<arch> [optional flags...]
```

내가 필요한건 macOS/window 애플리케이션이라 platform 옵션을 mac은 darwin, window용은 win32 만 사용했다. 아래를 참고.

<br/><br/>

***

<br/><br/>


# Supported Platforms
### Electron Packager is known to run on the following host platforms:

* Windows (32/64 bit)
* OS X (also known as macOS)
* Linux (x86/x86_64)

### It generates executables/bundles for the following target platforms:

* Windows (also known as `win32`, for both 32/64 bit)
* OS X (also known as `darwin`) 
/ [Mac App Store](https://electronjs.org/docs/tutorial/mac-app-store-submission-guide) (also known as `mas`)*
* Linux (for x86, x86_64, armv7l, arm64, and mips64el architectures)

_Note for OS X / MAS target bundles: the `.app` bundle can only be signed when building on a host OS X platform._

<br/><br/>

***

<br/><br/>

근데 여기서 win32 플랫폼을 사용하기 위해서는 wine이라는것이 필요한데 홈페이지에서 보면

> 와인(원래 “와인은 대리 실행기가 아니다.(Wine Is Not an Emulator)”의 머릿글자 입니다.)은 리눅스, 맥, BSD와 같은 POSIX 기반 운영체제에서 윈도우용 응용 무른모를 실행시키는 호환성 레이어입니다. 가상전산기나 대리 실행기처럼 윈도우 내부 시스템을 베껴오는 것 대신 와인은 윈도우 응용 무른모 프로그래밍 인터페이스를 POSIX 명령어로 곧바로 번역하여 성능과 메모리 문제를 해결해 다른 방식과는 차별화된 호환성을 제공합니다.

참고: [https://www.winehq.org/](https://www.winehq.org/)

여기서 다운받으면 되는지 알았는데, 계속 필요하다는 에러가 나와서 또 설치하는 방법을 찾아봤다. 이 페이지를 참고했다.

[https://www.davidbaumgold.com/tutorials/wine-mac/](https://www.davidbaumgold.com/tutorials/wine-mac/)

<br/>

지금까지 설치하지 않고 버티고 있었던 brew를 설치하고 wine을 설치해서 드디어 window용.exe 실행파일을 생성했다!

여기까지 실행한 결과 애플리케이션의 icon 모양이 electron의 모양이라 이걸 또 바꾸고 싶어서 불꽃 검색을 했다.

mac은 .icns 라는 확장자의 이미지가 필요하고, window는 .ico 라는 확장자를 가진 이미지가 필요하다. 이미지에서 확장자만 바꿔서 적용해 봤는데 파일 인식을 못하더라. 그래서 converting하는 페이지를 찾아서 이미지를 icns, ico 각각의 파일을 만들어서 저장해뒀다.

```
electron-packager <sourcedir> <appname> --platform=<platform> --arch=<arch> [optional flags...]
```

그럼 이 명령어에서 icon 옵션을 줄 수 있는데 여기에 이미지 path를 명시해주면 된다.

```
--icon=/path/image.icns(or ico)
```

그리고 나면 실행한 위치에 appname-[platform-x64] 과 같은 폴더가 생기고 그 안에 실행파일이 생성되어있다.

사실 가장 좋은 방법은 프로그램 폴더 안에서 프로그램을 build해서 electron으로 포팅해주면 가장 깔끔할 것 같은데, webpack 파일을 아직 자유자재로 다루지 못해서 이런 방법으로 애플리케이션을 만들게 되었다. 우선은 이렇게 사용해보고 계속해서 스터디를 해 볼 예정이다. 
~~혹시 webpack.config 파일에서 electron app위에 npm build, start 등을 할 수 있는 방법을 아신다면 알려주세요.~~