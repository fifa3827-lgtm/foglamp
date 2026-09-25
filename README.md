# 안개등 — 비 오는 항구의 탐정 이야기

흑백 느와르 퍼즐 게임. 방마다 누군가 남긴 흔적이 하나 있다. 빛을 비추고, 뒤집고, 닦고, 문지르고, 겹쳐서 읽는다. 읽은 것을 수첩에 적으면 다음으로 간다. 설명은 없다. 보는 사람만 본다.

**플레이:** https://fifa3827-lgtm.github.io/foglamp/

- 파일 하나(index.html)로 동작. PC는 전체화면, 모바일은 가로 화면. 진행은 기기에 저장된다.
- 5장 · 방 10개 · 두 갈래 결말. 1시간 안팎.

## 이 게임의 규칙 하나

글자가 나오는 데는 세 가지 이유만 있다. 원래 하나였던 것이 나뉘었거나(찢긴 사진, 먹지, 필름, 둘로 나눈 메시지), 누군가 일부러 그렇게 숨겼거나(격자 카드, 블라인드, 신호판, 거울 글씨), 물리적 흔적이거나(눌린 자국, 김 서린 유리, 비스듬한 빛). 우연히 겹쳐서 글자가 되는 일은 없다.

## 조작

- 물건은 끌 수 있다. 두드리면 뒤집히거나 열린다. 고른 물건 둘레의 붉은 고리를 끌면 돌아간다(PC는 마우스 휠로도 돈다).
- 오른쪽 아래 수첩에 읽은 낱말을 적는다. 맞으면 다음 방으로. 장이 끝나면 적은 낱말로 추리 문장을 완성한다(가짜 낱말이 섞인다).
- 힌트는 방마다 90초, 180초, 270초 뒤에 하나씩 열린다.

## 그림 — 제미나이로 만들어 넣기

`img/` 폴더에 아래 이름의 webp가 있으면 그 그림을 쓰고, 없으면 코드가 그린 절차 그림으로 동작한다. 한 장씩 넣어도 된다.
프롬프트와 파일 이름은 `tools/art/prompts.html` 에 있다. 받은 그림은 `python3 tools/prep-art.py <받은 폴더> img/` 로 흑백·크기·투명 배경을 맞춘다.

- 배경 `bg-01-office` … `bg-10-lamp-room` (1600×900)
- 장면 `s-01-city` … `s-15-dawn-lamp` (1600×900)
- 소품 `p-hat`, `p-glass`, `p-matchbox`, `p-lighter`, `p-carbon`, `p-card`, `p-key`, `p-pencil` … (투명 배경)

## BGM — 수노(Suno)로 만들어 넣기

`bgm/` 폴더에 아래 이름의 mp3를 넣으면 그 곡이 흐른다. 없으면 브라우저가 합성한 대체음이 나온다. 모두 **가사 없는 연주곡(instrumental)**, 2~3분, 반복 재생 전제.

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

## 만드는 방식

- `index.html` 하나에 그림 재료(art), 엔진(engine), 이야기(story), 방(rooms, rooms2)이 들어 있다. 원본은 `tools/` 에 나뉘어 있고 `node build.js`로 합친다.
- 방마다 정답 상태를 자동으로 만들어 보는 검증(`solve.js`)과, 타이틀부터 결말까지 자동으로 진행하는 검증(`flow.js`)을 통과했다.

## 정답표 (진행자용 — 플레이 전에는 읽지 말 것)

| 방 | 낱말 | 장치 | 누가 왜 |
|---|---|---|---|
| 1 탐정 사무소 | 고양이 | 블라인드 줄을 당겨 위에서 64% 높이에서 멈추면 창의 실금이 글자로 모인다 | 서연이 낮에 다녀가며 창에 긁었다. 쪽지는 관리인이 읽으니까 |
| 2 사무소, 정전 | 이수 | 라이터를 압지 둘레에서 120~500px 거리로 낮게 비춘다. 세로획은 옆빛, 가로획은 위아래 빛에서 보인다 | 서연이 책상에서 쪽지를 쓰고 가져갔다. 눌린 자국은 남는다 |
| 3 바 카운터 | 파도 | 먹지를 두드려 뒤집고 카운터 끝 램프 앞으로 | 이수가 주문지에 적어 손님에게 줬다. 윗장은 갔고 먹지가 남았다 |
| 4 바 뒷방 | 구층 | 구멍 뚫린 카드를 곡목표에 딱 맞춰 올린다. 파인 모서리가 고양이 자리(왼쪽 위). 다른 방향은 일층 앞방·삼층 옆방·지하 창고로 읽힌다 | 이수가 건넨 격자 암호 |
| 5 호텔 객실 | 창고 | 휴지통을 두드려 사진 조각 셋을 쏟고 찢긴 선대로 맞춘다. 간판 「해무 창고」 | 도현이 찢어 버렸다 |
| 6 호텔 욕실 | 장부 | 창을 닫고(두드림) 더운물 꼭지를 튼다(두드림). 김이 차면 손가락 글씨가 뜬다. 물탱크를 두드리면 열쇠 | 서연이 방이 뒤져질 것을 알고 거울에 썼다 |
| 7 부두 창고 | 서연 | 필름을 두드려 뒤집고 천장 램프 아래로, 그 위에 돋보기를 댄다 | 이름을 칠한 사람은 필름까지는 생각하지 못했다 |
| 8 창고 사무실 | 등대 | 연필을 끌어 오른쪽 페이지를 고르게 문지른다. 「만복 — 등대」, 만복은 가짜 낱말 | 뜯긴 장 아래 장의 눌린 자국 |
| 9 등대 계단 | 렌즈 | 열쇠로 상자를 열면(두드림) 신호판. 라이터를 아래, 판을 그 위에. 판이 라이터에 가까울수록 벽의 글자가 커진다. 판 각도 0°, 뒤집지 않음 | 등대지기가 배에 글자를 보내던 판 |
| 10 등대 꼭대기 | 도현 | 성냥갑을 두드려 필름을 꺼내 렌즈 틀의 필름 위에 정확히(각도 1도 단위) 겹친다 | 서연과 아버지가 둘로 나눈 메시지 |

추리 문장: 1장 「고양이·이수」 2장 「파도·구층」 3장 「장부·창고」 4장 「서연·등대」(가짜 「만복」) 5장 「렌즈·도현」(가짜 「서연」).
