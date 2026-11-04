# agent-skills

개인 Agent Skills 저장소. 필요할 때만 골라 설치한다.

[Agent Skills](https://agentskills.io) 형식. `npx skills`가 `skills/<name>/SKILL.md`를 찾아 설치한다.

## 설치

```bash
# 목록만 보기
npx skills add initred/agent-skills --list

# 하나만
npx skills add initred/agent-skills --skill git-commit

# 전부
npx skills add initred/agent-skills
```

모든 프로젝트에서 쓰려면 `-g`를 붙인다.

```bash
npx skills add initred/agent-skills --skill git-commit -g
```

로컬 클론에서 설치할 수도 있다.

```bash
npx skills add /Users/initred/Code/initred/agent-skills --skill git-commit
```

### Claude Code

Claude Code만 대상으로 설치하려면 `-a claude-code`를 붙인다. 이 프로젝트는 `.claude/skills/`, `-g`는 `~/.claude/skills/`에 들어간다.

```bash
# 이 프로젝트만
npx skills add initred/agent-skills --skill git-commit -a claude-code

# 모든 프로젝트
npx skills add initred/agent-skills --skill git-commit -a claude-code -g
```

스킬 폴더를 직접 복사해도 된다.

```bash
# 개인 (모든 프로젝트)
cp -r skills/git-commit ~/.claude/skills/git-commit

# 이 프로젝트만 (팀과 공유하려면 커밋)
mkdir -p .claude/skills
cp -r skills/git-commit .claude/skills/git-commit
```

설치 후 새 세션에서 `/commit`으로 호출하거나, 커밋해 달라고 하면 자동으로 쓴다.

### Codex

Codex만 대상으로 설치하려면 `-a codex`를 붙인다. 이 프로젝트는 `.agents/skills/`, `-g`는 `~/.agents/skills/`에 들어간다.

```bash
# 이 프로젝트만
npx skills add initred/agent-skills --skill git-commit -a codex

# 모든 프로젝트
npx skills add initred/agent-skills --skill git-commit -a codex -g
```

#### git-commit을 Luna 모델로 실행하기

Codex 스킬에는 모델을 지정하는 필드가 없다. 대신 모델을 지정한 커스텀 에이전트 [`git_committer`](codex/agents/git-committer.toml)(`gpt-5.6-luna`, 추론 강도 `low`)를 설치하면 스킬이 커밋 작업을 이 에이전트에 넘긴다. 에이전트 파일이 없으면 스킬은 현재 세션 모델로 실행된다.

```bash
# 개인 (모든 프로젝트)
mkdir -p ~/.codex/agents
curl -fsSL https://raw.githubusercontent.com/initred/agent-skills/main/codex/agents/git-committer.toml \
  -o ~/.codex/agents/git-committer.toml

# 이 프로젝트만
mkdir -p .codex/agents
curl -fsSL https://raw.githubusercontent.com/initred/agent-skills/main/codex/agents/git-committer.toml \
  -o .codex/agents/git-committer.toml
```

로컬 클론에서는 복사하면 된다.

```bash
cp codex/agents/git-committer.toml ~/.codex/agents/
```

설치 후 새 Codex 세션에서 커밋해 달라고 하면 `git_committer` 에이전트가 실행된다. 다른 모델을 쓰려면 파일의 `model` 값을 바꾼다.

## Skills

| Skill | 용도 |
| --- | --- |
| [`git-commit`](skills/git-commit/SKILL.md) | Conventional Commits. diff 분석, 스테이징, `git commit` 실행. `/commit` |

## 스킬 추가

```
skills/
  <skill-name>/
    SKILL.md
```

- 폴더 이름과 frontmatter `name`이 같아야 한다.
- `description`에는 무엇을 하는지와 언제 쓰는지(트리거 문구)를 넣는다.
- 에이전트용 지시만 둔다. README는 이 저장소 루트에만 둔다.

## License

[MIT](LICENSE)
