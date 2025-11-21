# 한국 역사 탐험 앱 (Korea History Explorer App)

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

[releases 페이지에서 최신 APK 다운로드](https://github.com/yourusername/historyapp/releases)

---

## 🌟 느낀점

우아한테크코스 프리코스를 진행하면서 자바에서 코틀린으로 넘어갈 때의 **언어의 간결함과 안전성**을 깊이 느꼈습니다.

처음에는 서버 개발만 경험했지만, 이번 프로젝트에서 **모바일 클라이언트까지 개발**하면서 같은 언어로 풀스택 애플리케이션을 만드는 경험이 매우 의미있었습니다.

특히 다음 부분들이 개발 과정에서 큰 깨달음을 줬습니다:

### 🔍 기술적 도전과 해결

**문제 1: 413 Request Entity Too Large 에러**
- 사용자가 업로드한 5-10MB 이미지가 서버에서 거부되는 문제 발생
- 비트맵 스케일링(1200x1200) + JPEG 80% 압축으로 **95% 크기 감소**
- 단순한 버그 처리가 아닌 시스템 전체의 효율성을 생각하는 경험

**문제 2: 팝업 다이얼로그 투명성 이슈**
- 모달 팝업 배경이 투명해서 텍스트가 보이지 않는 문제
- CardView + Window dimming (FLAG_DIM_BEHIND) 조합으로 해결
- UI/UX의 세부사항이 사용자 경험에 얼마나 중요한지 체감

### 💡 코틀린의 매력

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

코틀린의 **scope function** (`let`)과 **null safety**로 안전하고 간결한 코드 작성의 즐거움을 느꼈습니다.

### 🎨 디자인 통일성의 중요성

처음에는 각 화면이 독립적으로 설계되었지만, 프로젝트 진행 중 **일관된 디자인 언어**의 중요성을 깨달았습니다.

- 모든 화면에 동일한 헤더 (#D4A574)
- 한반도 지도 배경으로 주제 통일
- Material Design 3의 elevation과 corner radius로 시각적 계층 구조

이렇게 작은 세부사항들이 모여 **전문적이고 일관된** 애플리케이션을 만드는 경험이 매우 값졌습니다.

### 🚀 결론

**"같은 언어로 서버와 클라이언트를 개발하면서 느낀 통일성과, 작은 버그들을 하나씩 해결하면서 배운 디버깅 능력이 가장 큰 수확입니다."**

더 이상 특정 플랫폼에 제한받지 않고, 풀스택 개발자로서의 가능성을 보았습니다.

---

## 🛠️ 기술 스택

- **언어**: Kotlin 1.9
- **최소 SDK**: Android 12 (API 31)
- **UI**: ConstraintLayout, CardView, RecyclerView
- **네트워킹**: Retrofit 2, OkHttp3
- **이미지**: Picasso
- **인증**: JWT + Kakao SDK
- **디자인**: Material Design 3

---

