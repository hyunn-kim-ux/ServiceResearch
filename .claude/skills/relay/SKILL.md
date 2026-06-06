---
name: relay
description: summary/ 폴더 최신 파일을 Slack 지정 채널에 메시지로 게시한다.
---

## 설정

- Slack 워크스페이스: dailybrief-hq
- Slack 채널 ID: C0B8NDT4H9B
- 채널 URL(참고): https://dailybrief-hq.slack.com/archives/C0B8NDT4H9B

## 작업 순서

1. `summary/` 폴더에서 가장 최근에 추가된 `YYYY-MM-DD.md` 파일을 찾아 읽어라.
2. `slack_send_message`로 채널 `C0B8NDT4H9B`에 다음을 게시하라:
   - 첫 줄(헤더): `*[일일 브리핑] YYYY-MM-DD*`
   - 본문: summary 파일 내용 전체를 Slack mrkdwn 형식으로 변환하여 첨부
     - `**굵게**` → `*굵게*`
     - `*기울임*` → `_기울임_`
     - `# / ## / ###` 헤딩 → `*굵게*` 한 줄로 변환 (Slack에는 헤딩 문법 없음)
     - `[텍스트](URL)` → `<URL|텍스트>`
     - 목록(`- `, `1. `)·인용(`> `)·코드블록(```)는 그대로 사용 가능
3. 메시지가 Slack 단일 메시지 한도(약 40,000자)에 근접하면, 항목 단위 경계에서 여러 메시지로 분할 전송하라. 두 번째 이후 메시지는 같은 채널에 이어 보내라.
4. 전송 성공 응답(`ts` 또는 메시지 permalink)을 확인한 뒤 종료하라.

## 금지 사항

- GitHub에 추가 커밋 금지 (relay는 읽기·발송만 담당)
- 메시지 본문 임의 요약·재작성 금지 (mrkdwn 변환은 형식 변환만, 의미·문장 보존)
- summary 파일 수정·삭제 금지
- 채널을 임의로 변경 금지 (설정 섹션의 채널 ID만 사용)
