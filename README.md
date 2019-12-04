# android-ci-image

This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool like GitLab CI (Android SDK, NDK, git, fastlane). Make sure your CI environment's caching works as expected, this greatly improves the build time, especially if you use multiple build jobs.

Use generated public key as gitlab deploy key

```
docker run -it --rm jenshen1992/android-ci
cat ~/.ssh/id_rsa
```

A `.gitlab-ci.yml` with caching of your project's dependencies would look like this:

```
image: jenshen1992/android-ci

stages:
- build

before_script:
- export GRADLE_USER_HOME=$(pwd)/.gradle
- chmod +x ./gradlew

cache:
  key: ${CI_PROJECT_ID}
  paths:
  - .gradle/

build:
  stage: build
  script:
  - ./gradlew assembleDebug
  artifacts:
    paths:
    - app/build/outputs/apk/app-debug.apk
```


update:
1.3 = new version
 
 $docker build -t jenshen1992/android-ci:1.3 .
 $docker images
 
 $docker tag 7925878baad1 jenshen1992/android-ci:1.3
 
 $docker push jenshen1992/android-ci:1.3
 
