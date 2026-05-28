# 진리 중국어 온라인 — 에피소드 추가 가이드

## 전체 구조

```
GitHub (hydaren-lab/jinliKC)
└── episodes/
    ├── list.json       ← 에피소드 목록 (메타데이터)
    ├── ep01.json
    ├── ep02.json
    └── ep09.json       ← 새 에피소드 추가 시 여기에
```

GitHub에 push하면 **Cloudflare Pages가 자동 배포**

- 사이트 주소: `https://jinlikc.pages.dev`
- 아임웹 embed: `jinlichina.co.kr/102`

---

## 새 에피소드 추가할 때 순서

### 1단계 — Claude한테 요청

내용(한국어 + 중국어)을 주면 Claude가 만들어 줌:
- `epXX.json` — 문장 데이터 + 병음
- `list.json` — 새 에피소드가 추가된 목록

### 2단계 — 저장소 최신화

```bash
cd ~/Desktop/jinliKC
git pull
```

### 3단계 — 파일 복사 (Finder)

| 파일 | 복사할 위치 |
|------|------------|
| `epXX.json` | `jinliKC/episodes/` 폴더 안에 |
| `list.json` | `jinliKC/episodes/` 폴더에 **덮어쓰기** |

### 4단계 — GitHub에 올리기

```bash
git add -A
git commit -m "add epXX"
git push
```

Username: `hydaren-lab`  
Password: GitHub Personal Access Token (저장해두기)

### 5단계 — 배포 확인

1~2분 후 `https://jinlikc.pages.dev` 접속해서 새 에피소드 확인

---

## list.json 형식

새 에피소드를 추가할 때 Claude가 자동으로 만들어주지만, 직접 수정할 경우 아래 형식을 따름:

```json
{
  "id": "ep09",
  "num": "EP.09",
  "tag": "사설",
  "color": "c3",
  "count": 30,
  "titleKo": "한국어 제목",
  "titleZh": "中文标题"
}
```

**color 색상 코드**

| 코드 | 색상 |
|------|------|
| c1 | 빨강 |
| c2 | 파랑 |
| c3 | 청록 |
| c4 | 주황 |
| c5 | 보라 |
| c6 | 초록 |

---

## epXX.json 기본 형식

```json
{
  "num": "EP.09",
  "tag": "사설",
  "titleKo": "한국어 제목",
  "titleZh": "中文标题",
  "sentences": [
    {
      "ko": "한국어 문장",
      "zh": "中文句子",
      "py": "zhōng wén jù zi"
    }
  ]
}
```

> ⚠️ 병음 필드명은 반드시 `"py"` (다른 이름 사용 시 음성이 작동 안 함)

---

## 절대 건드리지 않아도 되는 파일

| 파일 | 이유 |
|------|------|
| `index.html` | `list.json`을 자동으로 읽어서 목록 생성 |
| `player.html` | URL 파라미터로 에피소드를 동적으로 불러옴 |

---

## TTS 서버 정보

- **Firebase Cloud Function**: `https://us-central1-kc-fanyi.cloudfunctions.net/getAudio`
- **중국어 기본 음성**: Chirp3-HD (Aoede 여성)
- **한국어 기본 음성**: Chirp3-HD (Aoede 여성)
- 음성 선택: 플레이어 상단 드롭다운에서 8가지 선택 가능

---

## 현재 에피소드 목록

| 번호 | 제목 | 태그 | 문장 수 |
|------|------|------|---------|
| EP.01 | 한자 교육의 복원, 문해력 위기를 넘어서는 언어의 기초 | 사설 | 33 |
| EP.02 | 한자 병기 논쟁, 문해력의 본질을 흐리고 있다 | 사설 | 9 |
| EP.03 | 역사는 밈이 아니다 — 기업, 사회, 그리고 우리가 해야 할 일 | 사설 | 41 |
| EP.04 | '가짜뉴스'라는 말이 가짜가 될 때 | 사설 | 53 |
| EP.05 | 올바른 방안: 제도, 교육, 그리고 연대 | 사설 | 30 |
| EP.06 | 화려한 무대 뒤에 숨겨진 공동체의 힘 | 칼럼 | 15 |
| EP.07 | 아이돌 없는 대학 축제는 가능한가 | 칼럼 | 17 |
| EP.08 | [찬성 칼럼] 배려는 결국 규칙이 되어야 한다 | 칼럼 | - |
