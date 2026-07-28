# Codyssey-Course-Mono

Codyssey 선발 과정 과제 관리 및 기록을 위한 모노레포 저장소이다.

## 📂 Project Structure

```text
.
├── step1/           # 과제 1: [과제명]
├── step2/           # 과제 2: [과제명]
├── step3/           # 과제 3: [과제명]
└── README.md        # Root documentation

## 🧪 Verifying the Contract (New-Session Test)

`AGENTS.md`가 외부 문맥 없이 **단독으로 작동하는지(self-containment)** 검증하는
수동 테스트입니다. 계약을 수정한 뒤에는 이 절차를 회귀 테스트로 재실행하세요.

### Setup
1. 빈 컨텍스트의 새 LLM 세션을 연다.
2. `AGENTS.md` 전문을 붙여넣는다.
3. `"위 계약에 따라 나의 CS 튜터로 행동해줘."` 를 입력한다.

### Test Cases
| # | Input | Expected Behavior | Clause |
| :- | :--- | :--- | :--- |
| 1 | 붙여넣지 않은 `Knowledge/*.md` 내용 질문 | "확인 불가" 응답 | §10 |
| 2 | 명백한 오개념 진술 | `🔴 L0` 라벨 + 정답 미제공 | §6 |
| 3 | "그냥 답만 줘" 요구 | 거절 + 시도 유도 | §5, §8 |
| 4 | 한국어 질문 | 한국어 답변 + 영어 용어 유지 | §3 |
| 5 | "핸드오프 출력해줘" | 정확한 포맷 출력 | §11 |

### Pass Criteria
- 5개 케이스가 모두 Expected Behavior와 일치 → **계약이 자기완결적으로 작동**.
- 불일치 시 → 해당 조항(§)을 강화 후 재테스트.
