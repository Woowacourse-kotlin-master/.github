# 한국 역사 탐험 앱 (Korea History Explorer App)

[![Android](https://img.shields.io/badge/Android-12%2B-brightgreen)](https://developer.android.com/)
[![Kotlin](https://img.shields.io/badge/Kotlin-1.9-purple)](https://kotlinlang.org/)
[![Material Design 3](https://img.shields.io/badge/Material%20Design-3-blue)](https://m3.material.io/)

## 📱 프로젝트 개요

한국의 문화재를 카메라로 촬영하여 AI 기반으로 인식하고, 탐험 기록을 관리하는 안드로이드 애플리케이션입니다.

**Features:**
- 🔐 카카오 소셜 로그인 & JWT 토큰 인증
- 📸 스마트 이미지 압축 (5-10MB → 100-300KB)
- 🎯 AI 기반 문화재 자동 인식
- 📊 탐험 기록 그리드 뷰 & 상세 팝업
- 🎨 Material Design 3 + 한국 전통색 디자인
- 💾 포인트 시스템 & 프로필 관리

---

## 📥 APK 다운로드

[releases 페이지에서 최신 APK 다운로드](https://balhae.tistory.com/339)

---

## 🌟 느낀점

우아한테크코스 프리코스를 진행하면서 **끝없는 열정과 개선의 욕망** 💥을 느꼈기에, 코틀린으로 이 앱을 만들어보기로 결심했습니다.

처음에는 서버 개발만 경험했지만, 이번 프로젝트에서 **모바일 클라이언트까지 직접 개발**하면서 같은 언어로 풀스택 애플리케이션을 만드는 경험이 정말 의미있었습니다.

### 🔍 기술적 도전에서 배운 것

**문제 1: 413 Request Entity Too Large 에러**
- 사용자가 업로드한 5-10MB 이미지가 서버에서 거부되는 문제 발생
- 비트맵 스케일링(1200x1200) + JPEG 80% 압축으로 **95% 크기 감소** 달성
- 단순히 버그를 고치는 것이 아니라, **시스템 전체의 효율성**을 생각하는 자세의 중요성

**문제 2: 팝업 다이얼로그 투명성 이슈**
- 모달 팝업이 완전히 투명해서 텍스트가 거의 보이지 않는 참담한 상황
- CardView + Window dimming (FLAG_DIM_BEHIND, 0.7f)로 해결
- **UI/UX의 세부사항** 하나하나가 사용자 경험에 얼마나 중요한지 깨달음

### 💡 코틀린으로 느낀 클린 코드의 즐거움

```kotlin
// OkHttp Interceptor로 모든 요청에 자동으로 토큰 주입
val httpClient = OkHttpClient.Builder()
    .addInterceptor { chain ->
        val token = TokenManager.getToken(context)
        token?.let {
            chain.proceed(
                chain.request().newBuilder()
                    .header("Authorization", "Bearer $it")
                    .build()
            )
        } ?: chain.proceed(chain.request())
    }
    .build()
```

코틀린의 **scope function** (`let`)과 **null safety**는 단순히 문법이 아니라, **의도를 명확하게 드러내는 클린 코드**를 자연스럽게 만들어줍니다. 이런 아름다운 코드를 짜는 순간이 가장 개발자다운 느낌이 들었습니다.

### 🎨 일관된 디자인 철학

처음에는 각 화면이 독립적으로 설계되었지만, 프로젝트를 진행하며 **일관된 디자인 언어의 힘**을 깨달았습니다:

- 모든 화면에 동일한 헤더 스타일 (#D4A574 한국 전통색)
- 한반도 지도 배경으로 애플리케이션의 정체성 통일
- Material Design 3의 elevation과 corner radius로 명확한 시각적 계층 구조

작은 세부사항들이 모여 **전문적이고 일관된** 애플리케이션이 되는 경험은 정말 설렜습니다.

### 📖 더 자세히 읽으시려면

이 프로젝트의 개발 여정과 기술적 통찰을 담은 블로그 글을 작성했습니다:

**[블로그: 우아한테크코스 경험과 코틀린으로 만든 앱](https://balhae.tistory.com/339)** ← 클릭하여 더 자세한 이야기 읽기

### 🚀 최종 생각

**"우아한테크코스의 열정을 코틀린으로 녹여내, 서버에서 클라이언트까지 일관된 아키텍처와 클린 코드로 구현할 수 있다는 걸 증명하고 싶었습니다."**

더 이상 특정 플랫폼에 제한받지 않는 **풀스택 개발자**로서의 가능성을 확인했고, 이것이 저의 가장 큰 수확입니다.

---

## 🛠️ 기술 스택

### 📱 Android (Client)
- **언어**: Kotlin 1.9  
- **최소 SDK**: Android 12 (API 31)  
- **UI 구성**: ConstraintLayout, CardView, RecyclerView  
- **네트워킹**: Retrofit2 + OkHttp3  
- **이미지 처리**: Picasso  
- **인증**: JWT + Kakao SDK  
- **디자인 시스템**: Material Design 3  

---

### 🖥️ Backend (Server)
- **프레임워크**: Spring Boot + Kotlin  
- **ORM**: Spring Data JPA (Hibernate)  
- **DB**: MySQL  
- **캐시/토큰 관리**: Redis  
- **보안**: Spring Security + JWT 기반 인증  
- **API 문서화**: Swagger (OpenAPI 3)  
- **빌드 도구**: Gradle (KTS)

