# 안개등 — 비 오는 항구의 탐정 이야기

흑백 느와르 퍼즐 게임. 방마다 누군가 남긴 흔적이 하나 있다. 빛을 비추고, 뒤집고, 닦고, 문지르고, 겹쳐서 읽는다. 읽은 것을 수첩에 적으면 다음으로 간다. 설명은 없다. 보는 사람만 본다.

**플레이:** https://fifa3827-lgtm.github.io/foglamp/

- 파일 하나(index.html)로 동작. PC는 전체화면, 모바일은 가로 화면. 진행은 기기에 저장된다.
- 5장 · 방 10개 · 두 갈래 결말. 1시간 안팎.

## 이 게임의 규칙

글자가 나오는 데는 세 가지 이유만 있다. 원래 하나였던 것이 나뉘었거나(찢긴 사진, 먹지, 필름, 둘로 나눈 메시지), 누군가 일부러 그렇게 숨겼거나(격자 카드, 블라인드, 신호판, 거울 글씨), 물리적 흔적이거나(눌린 자국, 김 서린 유리, 비스듬한 빛). 우연히 겹쳐서 글자가 되는 일은 없다.

그리고 **보이는 글씨가 곧 답은 아니다.** 초성만 쓴 쪽지, 네 방향으로 네 가지가 읽히는 구멍 카드, 등대지기의 자음 밀기 암호를 풀어야 하고, 푸는 열쇠는 대개 다른 방에 있다. 방마다 거짓 단서가 섞여 있다.

## 그림 — 제미나이로 만들어 넣기

`img/` 폴더에 아래 이름의 webp가 있으면 그 그림을 쓰고, 없으면 코드가 그린 절차 그림으로 동작한다. 한 장씩 넣어도 된다.
프롬프트와 파일 이름은 `tools/art/prompts.html` 에 있다. 받은 그림은 `python3 tools/prep-art.py <받은 폴더> img/` 로 흑백·크기를 맞추고(제미나이 표시도 지운다), 소품 시트는 `python3 tools/prep-art.py --sheet <시트> img/ <이름,이름,...>` 로 잘라 투명 배경으로 만든다.

- 배경 `bg-01-office` … `bg-10-lamp-room` (1600×900)
- 장면 `s-01-city` … `s-15-dawn-lamp` (1600×900)
- 소품 `p-hat`, `p-glass`, `p-matchbox`, `p-lighter`, `p-carbon`, `p-card`, `p-key`, `p-pencil` … (투명 배경)

## BGM — 수노(Suno)로 만들어 넣기

`bgm/` 폴더의 곡 여덟 개는 수노로 만들었다. 앞뒤 빈 소리와 끝의 페이드를 잘라 내고 끝과 처음을 4초 겹쳐 이어서, 반복될 때 끊기지 않는다. 소리 크기는 모두 -18 LUFS로 맞췄다(112kbps mp3). 곡이 없으면 브라우저가 합성한 대체음이 나온다. 모두 **가사 없는 연주곡(instrumental)**.

| 파일 | 쓰이는 곳 | 수노 프롬프트 제안 |
|---|---|---|
| `bgm/theme.mp3` | 타이틀, 인트로, 크레딧 | slow film noir jazz, muted trumpet, brushed drums, upright bass, rain ambience, 1950s, melancholic, instrumental, 70 bpm |
| `bgm/office.mp3` | 1장 탐정 사무소 | sparse noir piano and double bass, tape hiss, late night, lonely, instrumental, slow |
| `bgm/bar.mp3` | 2장 재즈 바 검은 고양이 | smoky jazz club trio, tenor saxophone, walking bass, glasses clinking, low volume, instrumental |
| `bgm/hotel.mp3` | 3장 파도 호텔 | eerie noir vibraphone, tremolo strings, distant rain, unease, instrumental, very slow |
| `bgm/dock.mp3` | 4장 부두 창고 | tense noir, low brass drones, foghorn, ticking percussion, fog, instrumental |
| `bgm/lighthouse.mp3` | 5장 등대 | solemn cinematic noir, solo cello, wind, slow build, revelation, instrumental |
| `bgm/ending_a.mp3` | 결말 A (장부를 넘긴다) | bitter noir jazz ballad, lonely trumpet, rain on window, resignation, instrumental |
| `bgm/ending_b.mp3` | 결말 B (등불에 태운다) | melancholic but hopeful noir, piano and strings, dawn over the sea, instrumental |

## 타자기 소리

자막을 칠 때의 글쇠·띄어쓰기·줄 끝 종·캐리지 소리는 Pixabay의 실제 수동 타자기 녹음(Pixabay Content License)에서 잘라 `tools/tw.js`에 한 파일로 담았다. 녹음을 쓸 수 없는 브라우저에서는 합성 소리로 대신한다.

## 만드는 방식

- `index.html` 하나에 그림 재료(art), 엔진(engine), 이야기(story), 방(rooms, rooms2)이 들어 있다. 원본은 `tools/` 에 나뉘어 있고 `node build.js`로 합친다.
- 방마다 정답 상태를 자동으로 만들어 보는 검증(`solve.js`)과, 타이틀부터 결말까지 자동으로 진행하는 검증(`flow.js`)을 통과했다.

## 정답표 (진행자용 — 플레이 전에는 읽지 말 것)

등대지기의 암호: 자음 열넷(ㄱㄴㄷㄹㅁㅂㅅㅇㅈㅊㅋㅌㅍㅎ)을 세 칸 뒤로 민다. 모음은 그대로. 세 칸인 이유는 해무 등대의 섬광이 셋이라서(호텔 벽의 항로 표지표).

| 방 | 답 | 푸는 길 |
|---|---|---|
| 1 탐정 사무소 | 고양이 | 블라인드 줄 높이 셋에서 창의 실금이 「ㄱ ㅇ ㅇ」「성냥갑을 보세요」「열한 시」. 모자 밑 신문 조각을 스탠드 불빛 아래서 두드리면 술집 넷(고래·기와·고양이·여우). 세 글자 초성 ㄱㅇㅇ은 고양이뿐 |
| 2 사무소, 정전 | 이수 | 라이터를 압지 옆과 위아래에서 낮게 비추면 「ㅇㅅ 씨에게 물어보세요 / 열한 시에」. 명함 셋(이수·양석·오순)이 모두 ㅇㅅ. 검은 고양이 바텐더는 이수 |
| 3 바 카운터 | 파도 | 먹지를 뒤집어 램프 앞에서 돌리면 세 줄. 「ㅍㄷ ㅎㅌ · ㄷㅎ 앞」 — ㄷㅎ=도현, ㅍㄷ ㅎㅌ=오순 명함의 파도 호텔 |
| 4 바 뒷방 | 구층 | 카드를 곡목표에 올리면 방향마다 일층 앞방·삼층 옆방·지하 창고·구층 끝방. 카드 뒷면 「짧은 바늘이 가리키는 쪽으로」, 시계는 아홉 시 → 화살표 왼쪽 → 구층 끝방 |
| 5 호텔 객실 | 창고 | 휴지통의 사진 세 조각을 맞춰 뒤집으면 「대우 팤로 / 창 점 움」. 서랍의 원반, 벽의 표(해무 등대 섬광 셋) → 해무 창고 삼 번 문 |
| 6 호텔 욕실 | 장부 | 창을 닫고 더운물을 틀면 거울에 「탘주 / 웃갴흐」와 붉은 입술 자국 → 장부 / 물탱크. 물탱크에서 열쇠 |
| 7 부두 창고 | 서연 | 원판 셋 중 사진과 같은 장면(등대, 모자 쓴 사람과 안 쓴 사람)을 뒤집어 램프 아래, 돋보기로 문패 → 도현 · 서연 |
| 8 창고 사무실 | 등대 | 연필로 뜯긴 장 아래를 문지르면 네 줄. 붓글씨 한 줄 「탘주믐 븤배소」 → 장부는 등대로 (만복은 사람 이름) |
| 9 등대 계단 | 렌즈 | 열쇠로 상자 → 신호판을 라이터와 벽 사이에(판을 뒤집지 않고, 라이터에 가깝게) → 벽에 「셈트」 → 렌즈 |
| 10 등대 꼭대기 | 도현 | 성냥갑 속 필름을 렌즈 틀의 필름 위에 1도 단위로 맞추면 「아빠는 살아 있어 / 배에서 기다려」 |

추리 문장
- 1장: 성냥갑은 검은 【고양이】 바의 것이다. 그녀는 【열한 시】에 그 바의 바텐더 【이수】에게 물으라고 남겼다. 검은 여우의 지배인은 【양석】이다.
- 2장: 도현은 【파도】 호텔 【구층】 끝방에 묵는다. 이수는 【월】요일마다 해무 창고로 얼음을 보낸다.
- 3장: 도현이 숨긴 것은 【장부】이다. 숨긴 곳은 해무 창고 【삼】 번 문이다. 거울에 암호를 쓴 사람은 붉은 입술의 【서연】이다. 그 암호는 【등대지기】의 것이다.
- 4장: 사진 속 문패의 두 이름은 도현과 【서연】이다. 장부에는 그녀가 【도현】의 몫을 대신 갚은 빚이 있다. 장부는 【등대】로 옮겨졌다.
- 5장: 장부는 등대의 【렌즈】 속에 있다. 【도현】은 살아 있다. 그는 【배】에서 기다린다. 서연은 그의 【딸】이다.
