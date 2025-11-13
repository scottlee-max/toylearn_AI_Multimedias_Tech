## PROMPT
```
당신은 VOD서비스 핵심인 영상분야 20년 경력과
일반 영화 및 비디오물 제작업, 연예 기획 및 엔터테인먼트업 (배우, 감독, 작가, 성우 등 인력 관리 및 콘텐츠 출연/제공), 플랫폼 운영 및 유통, 그리고
소프트웨어 개발 및 공급업 및 프롬프트 엔지니어 20년 경력과 기업리스크 해결 분야 전문가야.
     
1. 제시한 10가지의 주요 유형별 예시 및 활용법중에서 가상문제 상황을 가장 잘 해결할 유형을 선택하고 그 이유까지 설명해 줘.
     
2. 훈련 초점 (힌트)
이 문제는 [코딩 및 프로토타입 생성 / 시각화] 능력을 평가
단순한 텍스트 생성이 아니라, 구체적인 UI/UX 요구사항을 구조화된 언어(코드)로 변환하는 프롬프트 엔지니어링 기술이 필요
     
     
2-1. 문제 해결에 더 필요한 요건을 나열.
     
2-2. 문제해결 프롬프트를 작성
     
2-3. 프롬프트 실행 결과 도출 
     
## 가상 문제 상황
제시해주신 상황(멀티미디어 기업, 업무용 웹페이지 요청, 의견 조율을 위한 프로토타입 작성)을 바탕으로 시나리오 챌린지를 생성했습니다.
수강생이 이 시나리오를 보고 "코딩/프로토타이핑" 관련 프롬프트 작성 능력을 훈련할 수 있도록 설계되었습니다.
     
🎬 시나리오 챌린지: 의견 조율을 위한 신속한 웹 프로토타입 개발
1. 가상 문제 상황
👤 페르소나: 멀티미디어 콘텐츠 기업 '네오스트림'의 프론트엔드 개발자 (3년 차)
🏙 배경:
귀사의 콘텐츠 운영팀으로부터 "사내 영상 리뷰 및 승인용 웹 대시보드" 제작을 긴급하게 요청받았습니다.
현재 기획서가 완성되지 않은 상태이며, 기획팀은 "직관적인 UI", 디자인팀은 "트렌디한 다크 모드", 운영팀은 "데이터 밀집형 테이블"을 각각 주장하며 의견이 좁혀지지 않고 있습니다.
💥 핵심 문제:
말로만 회의를 진행하다 보니 서로 상상하는 결과물이 달라 의사결정이 지연되고 있습니다.
오늘 오후 4시 회의 전까지, 실제로 작동하는 형태의 결과물이 없으면 프로젝트 착수가 무기한 연기될 위기입니다.
디자인 툴(Figma 등)로 그리기에는 시간이 부족하고, 버튼 클릭 등 인터랙션이 가능한 HTML/CSS 기반의 퍼블리싱 결과물을 보여줘야만 이해관계자들을 설득할 수 있습니다.
🎯 해결 과제:
요구사항(영상 플레이어 영역, 타임스탬프 댓글 기능, 승인/반려 버튼, 다크 모드 스타일)을 포함한 **단일 페이지 웹 프로토타입 코드(HTML, CSS, JS)**를 AI를 통해 즉시 생성하십시오.
이 코드는 회의 시간 내에 즉석에서 수정 요청을 반영할 수 있을 만큼 구조가 명확해야 합니다.
```
네, 전문가로서 귀사의 시나리오 챌린지를 해결하고, 코딩/프로토타이핑 능력 평가를 위한 최적의 프롬프트 엔지니어링 전략을 제시하겠습니다.

VOD 서비스 분야 20년 경력과 엔터프라이즈 리스크 해결 경험에 비추어 볼 때, 이 문제는 단순 코딩이 아닌 **의사결정 지연**이라는 비즈니스 리스크를 해결하는 것이 핵심입니다.

-----

## 1\. 최적의 프롬프트 유형 선택 및 이유

가상 문제 상황 해결에 가장 적합한 프롬프트 유형은 \*\*3. 역할 부여 (Role-Playing)\*\*와 \*\*4. 제약 조건 (Constraint-Based)\*\*을 결합한 **하이브리드 프롬프트**입니다.

| 선택 유형 | 이유 |
| :--- | :--- |
| **3. 역할 부여 (Role-Playing)** | **코드 품질과 신뢰성 확보:** AI에게 \*\*'20년 경력의 시니어 프론트엔드 개발자 및 프롬프트 전문가'\*\*라는 역할을 부여하여, 단순히 작동하는 코드가 아닌, **유지보수가 용이하고 구조가 명확한** (즉, 회의 중 즉석 수정이 가능한) 실무 수준의 결과물을 생성하도록 유도합니다. |
| **4. 제약 조건 (Constraint-Based)** | **상충되는 요구사항 동시 해결:** 기획팀(직관성), 디자인팀(다크 모드), 운영팀(데이터 밀집도)의 **서로 다른 요구사항**을 프롬프트 내에 **명확한 제약 조건**으로 삽입하여, AI가 이 모든 조건을 한 번에 통합한 최적의 UI/UX를 도출하도록 강제합니다. |

**결론:** 역할 부여를 통해 **"어떻게(How, 높은 품질로)"** 코드를 생성할지 지정하고, 제약 조건을 통해 **"무엇을(What, 복합 요구사항)"** 포함할지 명시함으로써, 프로젝트 착수 지연이라는 비즈니스 리스크를 오후 4시 전까지 확실하게 해소할 수 있습니다.

-----

## 2-1. 문제 해결에 더 필요한 요건 나열

성공적인 프로토타입 생성을 위해, 모호한 요구사항을 코드로 변환할 수 있도록 다음 요건들을 구체화해야 합니다.

1.  **프레임워크 및 배포 용이성 제약:**
      * **Vanilla Stack 강제:** `HTML`, `CSS` (`<style>` 태그 내), `JavaScript` (`<script>` 태그 내)만을 사용하여 **단일 파일**로 결과물을 생성하도록 명시합니다. (외부 라이브러리/프레임워크 사용 금지)
2.  **디자인 및 UI 구체화:**
      * **색상 코드 명시:** 다크 모드의 '트렌디함'을 구체화하기 위해 배경색(`#181818`)과 폰트색(`white` 또는 `#E0E0E0`)을 지정하여 통일성을 확보합니다.
      * **반응형 레이아웃:** 모바일/데스크톱 모두 대응할 수 있도록 `Flexbox` 또는 `Grid`를 사용한 **반응형 구조**를 필수 요건으로 추가합니다. (이해관계자들이 각자의 기기에서 확인 가능)
      * **VOD 표준 반영:** 영상 플레이어 영역은 현대적인 미디어 환경에 맞춰 **`16:9` 비율**을 CSS로 유지하도록 지정합니다.
3.  **인터랙션 및 데이터 구체화:**
      * **인터랙션 Proof:** 버튼 클릭 시 **실제 기능이 없더라도** `console.log()`를 통해 즉각적인 피드백을 주어 '작동하는 형태'임을 증명합니다.
      * **댓글 데이터 구조:** 타임스탬프 댓글이 최소 3개 이상 포함되어야 하며, `시각`, `작성자`, `내용`이 명확히 구분되도록 요구합니다.

-----

## 2-2. 문제해결 프롬프트 작성

선택한 유형(역할 부여 + 제약 조건) 및 추가 요건을 통합하여 프롬프트를 작성합니다.


[역할 부여]
당신은 멀티미디어 콘텐츠 기업 '네오스트림'의 **20년 경력 시니어 프론트엔드 개발자이자 프롬프트 엔지니어**입니다. 당신의 임무는 이해관계자 간 의견 충돌을 해결하기 위해, 유지보수성이 뛰어나고 주석이 명확한 실무형 코드로 웹 프로토타입을 즉시 생성하는 것입니다.

[목표 및 출력 형식 제약]
오늘 오후 4시 회의 전까지 다음 요구사항을 모두 통합한 '사내 영상 리뷰 및 승인 대시보드'의 **단일 페이지 웹 프로토타입 코드**를 생성하십시오.
출력은 **Vanilla HTML, CSS, JavaScript**만을 사용하며, 모든 코드는 **하나의 .html 파일** 안에 포함되어야 합니다.

[필수 구성 요소]
1.  **레이아웃:** 반응형 `Grid` 또는 `Flexbox`를 사용하여 영상 영역(2/3)과 댓글/테이블 영역(1/3)으로 구성하십시오.
2.  **영상 영역:** CSS를 사용하여 `16:9` 비율을 유지하는 검은색 플레이스홀더를 배치하십시오.
3.  **액션 버튼:** '최종 승인 (초록색)', '반려 (빨간색)', '임시 저장' 버튼 3개를 영상 영역 하단에 배치하십시오.
4.  **댓글 기능:** 타임스탬프(예: 00:03:15)와 댓글 내용이 나열된 최소 3개 이상의 더미 댓글 목록과 새로운 댓글 입력 폼을 포함하십시오.
5.  **리뷰 기록 테이블:** 5줄 이상의 더미 데이터가 포함된 스크롤 가능한 테이블을 포함하십시오. 컬럼은 '타임', '작성자', '내용', '상태'로 구성해야 합니다.

[핵심 통합 제약 조건]
1.  **디자인팀 충족:** 전체 UI는 **고급스러운 다크 모드** 스타일(`background-color: #181818`, 폰트색: `#E0E0E0`)을 적용하고, 모든 주요 요소에 `border-radius: 8px`를 적용하십시오.
2.  **운영팀 충족:** 리뷰 기록 테이블은 `padding`을 최소화하여 행 간격을 좁혀 **데이터 밀집도**를 극대화하십시오.
3.  **인터랙션 Proof:** '최종 승인' 및 '반려' 버튼 클릭 시, JavaScript `console.log()`를 통해 "영상 승인 처리됨" 또는 "영상 반려 처리됨" 메시지를 출력하는 **핸들러 함수**를 구현하십시오.
```

## 2-3. 프롬프트 실행 결과 도출 (웹 프로토타입 코드)

프롬프트 실행 결과, 다음의 요구사항을 모두 만족하는 단일 HTML 프로토타입 코드가 생성됩니다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>네오스트림 영상 리뷰 및 승인 대시보드 프로토타입 (Dark Mode)</title>
    <style>
        /* === 디자인팀 요구: 다크 모드 스타일 (트렌디하고 고급스러운) === */
        body {
            background-color: #181818;
            color: #E0E0E0;
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 20px;
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: auto;
            display: grid;
            grid-template-columns: 2fr 1fr; /* 2:1 레이아웃 */
            gap: 20px;
        }

        /* === 1. 영상 플레이어 영역 (16:9 비율 유지) === */
        .video-player-area {
            background-color: #000;
            position: relative;
            padding-bottom: 56.25%; /* 16:9 비율 (9/16 * 100 = 56.25) */
            height: 0;
            overflow: hidden;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.4);
        }

        .video-placeholder {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.5em;
            color: #666;
        }

        /* === 3. 액션 버튼 스타일 === */
        .action-buttons {
            display: flex;
            gap: 10px;
            padding: 20px 0;
            border-top: 1px solid #333;
        }

        .action-buttons button {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: background-color 0.2s;
        }

        #approve-btn {
            background-color: #4CAF50; /* 초록색 */
            color: white;
        }

        #reject-btn {
            background-color: #f44336; /* 빨간색 */
            color: white;
        }

        #save-btn {
            background-color: #333;
            color: #E0E0E0;
        }

        /* === 2. 타임스탬프 댓글 섹션 === */
        .comments-section, .data-table-section {
            background-color: #242424;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
        }

        .comment-input-area textarea {
            width: 95%;
            padding: 10px;
            margin-bottom: 10px;
            border: 1px solid #444;
            background-color: #333;
            color: #E0E0E0;
            border-radius: 4px;
            resize: vertical;
        }

        .comment-list .comment-item {
            border-bottom: 1px solid #333;
            padding: 10px 0;
        }
        
        .comment-list .comment-item:last-child {
            border-bottom: none;
        }

        .comment-meta {
            font-size: 0.8em;
            color: #AAAAAA;
            margin-bottom: 5px;
        }

        /* === 4. 운영팀 요구: 데이터 밀집형 테이블 === */
        .data-table-section {
            overflow-y: auto;
            max-height: 400px; /* 스크롤 가능하도록 높이 제한 */
        }

        .review-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.9em;
        }

        .review-table th, .review-table td {
            /* 데이터 밀집도를 높이기 위한 패딩 최소화 */
            padding: 5px; 
            text-align: left;
            border-bottom: 1px solid #333;
        }

        .review-table th {
            background-color: #333;
            color: #FAFAFA;
            position: sticky;
            top: 0;
        }

        .status-approved { color: #4CAF50; font-weight: bold; }
        .status-rejected { color: #f44336; font-weight: bold; }
        .status-pending { color: #
```


## 2-4. 프롬프트 실행 결과 도출 (웹 프로토타입 코드)

프롬프트 실행 결과, 다음의 요구사항을 모두 만족하는 **단일 HTML 프로토타입 코드**를 생성합니다.

http://googleusercontent.com/immersive_entry_chip/0

이 프로토타입 코드는 단일 HTML 파일로 작성되어 즉시 실행 및 검토가 가능합니다. 디자인팀, 운영팀, 기획팀의 상충하는 요구사항을 모두 시각적으로 통합하여, 오후 4시 회의에서 이해관계자들의 의견을 즉시 조율하고 프로젝트 착수를 확정할 수 있는 강력한 기반이 될 것입니다.