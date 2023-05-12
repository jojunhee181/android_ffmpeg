# android_ffmpeg

안드로이드 ffmpeg build 기록을 위한 프로젝트. ( for Mac )

NDK
1. https://developer.android.com/ndk/downloads?hl=ko 에서 ndk 다운로드 (21e 버전 사용)

FFMPEG
1. https://ffmpeg.org 에서 ffmpeg 소스 다운로드. (6.0 버전으로 다운로드 했음)
2. build_android.sh 파일을 만들어 집어넣음(프로젝트에 등록하 것 복사).
- ndk 경로를 넣어주는 것 중요.
3. build_android.sh 빌드
- 빌드 완료시 android 폴더 생성됨

Android
1. 앱 폴더 최상단에 lib 폴더 추가.
2. 해당 폴더에 빌드 했던 arm64-v8a(64bit), armeabi-v7a(32bit 빌드시 넣음) 를 넣음.
3. src/main/ 폴더에 cpp 폴더를 만듬.
4. CMakeLists.txt 를 만들고 위에 기재했던 library를 링크시킴.
5. 동작시킬 cpp 코드를 같은 폴더에 생성 시키고 CMakeList.txt 에서 링크시킴.
6. build.gradle 파일에 다음과 같이 기재
- defaultConfig{
 ...
 ndk{
  abiFilters 'arm64-v8a'
 }
}

sourceSets{
  main{
  jniLibs.srcDirs = ['라이브러리 경로']
  }
}

externalNativeBuild{
  cmake{
    path file('src/main/cpp/CmakeLists.txt')
    version '3.22.1'  
  }
}
