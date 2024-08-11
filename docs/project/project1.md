---
layout: default
title: Project1
parent: Project
nav_order: 1
---

# 스텔라이브 키리누키 사이트

## 2024_08_10

우선 키리누키 사이트를 만들기 위해 첫번째로 해야할일은 목표를 설정하는 것이었다.

이 프로젝트를 기획한 이유는 아래와 같았다.

1. 너무 많은 키리누키 채널들을 일일히 찾지 않도록 모으자

2. 나의 최애를 모아보자

그래서 다음과 같이 목표를 잡고 진행하기로 했다.

{: .important }
**🎯 목표** : 유튜브에 있는 모든 스텔라이브 키리누키 채널을 쉽게 모아서 볼수있는 웹사이트

그렇다면 기능은 무엇이 필요할까?

**주요기능**

- 모든 키리누키 채널을 모으는 기능
- 해당 영상이 어떤 스텔라이브 멤버인지 확인하고 분류하는 기능

**서브기능**

- 최신 업데이트 영상 알림 기능
- 좋아요, 날짜 등 정렬하는 기능

우선은 이정도 기능만 구현하고 추후 발전 시켜보자

작업시작하기 전 TO DO 리스트 작성도 대략 해보자

TO-DO List

1. ~~기능 생각해보기~~
   {: .d-inline-block }
   완료 {: .label .label-green }

2. 유튜브 키 발급 받기
3. 유튜브 api 살펴보기
4. 기능 명세서 작성
5. 와이어 프레임 제작
6. ui 제작
7. 백엔드 문서 작성
8. 프론트엔드 문서 작성
9. 백엔드 api 완성 시키기
10. 프론트엔드 짬짬히 완성

### 유튜브 API 살펴보기

유튜브에서는 개발자에게 유튜브 API를 제공한다,
[유튜브 API docs 바로가기!](https://developers.google.com/youtube/v3/getting-started?hl=ko#%EC%98%88-2){: .btn }

[유튜브 API 사용해보기!](https://developers.google.com/youtube/v3/docs/channels/list?apix=true&hl=ko&apix_params=%7B%22part%22%3A%5B%22snippet%2CcontentDetails%2Cstatistics%22%5D%2C%22forHandle%22%3A%22%40user-nm1id1hr8f%22%7D){: .btn }

키를 발급 받고 사용하면 되는데 우선 키를 받기 전 내가 구현하고 싶은 기능들을 구현 가능한지 체크하고 넘어가자

**채널 정보 받아오기**

```http
GET https://youtube.googleapis.com/youtube/v3/channels?part=snippet%2CcontentDetails%2Cstatistics&forHandle=%40user-nm1id1hr8f&key=[YOUR_API_KEY] HTTP/1.1

Authorization: Bearer [YOUR_ACCESS_TOKEN]
Accept: application/json
```

```json
{
  "kind": "youtube#channelListResponse",
  "etag": "q8-FfK-xVBO8g8cgIday2IuE7rg",
  "pageInfo": {
    "totalResults": 1,
    "resultsPerPage": 5
  },
  "items": [
    {
      "kind": "youtube#channel",
      "etag": "gk9nYBqrRrBvvptWJpNt5iIn0Us",
      "id": "UCSkxf8rEikMXb5Bgc92u_lQ",
      "snippet": {
        "title": "유니 발닦개",
        "description": "스텔라이브 \"팬페이지\"  입니다.  \n\n피드백 및 불만사항등등 : djdejd235@gmail.com \n",
        "customUrl": "@user-nm1id1hr8f",
        "publishedAt": "2022-01-22T18:05:04.398155Z",
        "thumbnails": {
          "default": {
            "url": "https://yt3.ggpht.com/BuTK3zR07vGMcjGDf4J12g1QZEAGf_hti7Q4O4vSpCY5z4eOGQgV1_7viGm-Q5VUmxGLGelKa_0=s88-c-k-c0x00ffffff-no-rj",
            "width": 88,
            "height": 88
          },
          "medium": {
            "url": "https://yt3.ggpht.com/BuTK3zR07vGMcjGDf4J12g1QZEAGf_hti7Q4O4vSpCY5z4eOGQgV1_7viGm-Q5VUmxGLGelKa_0=s240-c-k-c0x00ffffff-no-rj",
            "width": 240,
            "height": 240
          },
          "high": {
            "url": "https://yt3.ggpht.com/BuTK3zR07vGMcjGDf4J12g1QZEAGf_hti7Q4O4vSpCY5z4eOGQgV1_7viGm-Q5VUmxGLGelKa_0=s800-c-k-c0x00ffffff-no-rj",
            "width": 800,
            "height": 800
          }
        },
        "localized": {
          "title": "유니 발닦개",
          "description": "스텔라이브 \"팬페이지\"  입니다.  \n\n피드백 및 불만사항등등 : djdejd235@gmail.com \n"
        },
        "country": "KR"
      },
      "contentDetails": {
        "relatedPlaylists": {
          "likes": "",
          "uploads": "UUSkxf8rEikMXb5Bgc92u_lQ"
        }
      },
      "statistics": {
        "viewCount": "22726713",
        "subscriberCount": "18900",
        "hiddenSubscriberCount": false,
        "videoCount": "949"
      }
    }
  ]
}
```

채널 정보는 위와같이 가져올수 있다. 필요한 정보는 다가져오는거 같다. (채널대상! ㅣ 유니 발닦개님)
