# ARM Coding Worker Skill

```
@@@@@@   @@@@@@@   @@@@@@@@@@      @@@  @@@   @@@@@@   @@@@@@@   @@@  @@@  @@@@@@@@   @@@@@@    @@@@@@
@@@@@@@@  @@@@@@@@  @@@@@@@@@@@     @@@  @@@  @@@@@@@@  @@@@@@@@  @@@@ @@@  @@@@@@@@  @@@@@@@   @@@@@@@
@@!  @@@  @@!  @@@  @@! @@! @@!     @@!  @@@  @@!  @@@  @@!  @@@  @@!@!@@@  @@!       !@@       !@@
!@!  @!@  !@!  @!@  !@! !@! !@!     !@!  @!@  !@!  @!@  !@!  @!@  !@!!@!@!  !@!       !@!       !@!
@!@!@!@!  @!@!!@!   @!! !!@ @!@     @!@!@!@!  @!@!@!@!  @!@!!@!   @!@ !!@!  @!!!:!    !!@@!!    !!@@!!
!!!@!!!!  !!@!@!    !@!   ! !@!     !!!@!!!!  !!!@!!!!  !!@!@!    !@!  !!!  !!!!!:     !!@!!!    !!@!!!
!!:  !!!  !!: :!!   !!:     !!:     !!:  !!!  !!:  !!!  !!: :!!   !!:  !!!  !!:            !:!       !:!
:!:  !:!  :!:  !:!  :!:     :!:     :!:  !:!  :!:  !:!  :!:  !:!  :!:  !:!  :!:           !:!       !:!
::   :::  ::   :::  :::     ::      ::   :::  ::   :::  ::   :::   ::   ::   :: ::::  :::: ::   :::: ::
 :   : :   :   : :   :      :        :   : :   :   : :   :   : :  ::    :   : :: ::   :: : :    :: : :
```

[![skills.sh](https://skills.sh/b/armcompany/arm-coding-worker-skill)](https://skills.sh/armcompany/arm-coding-worker-skill)

Autonomous software engineering skill for coding agents. Delivers verified repository changes as an autonomous software engineer — works standalone from sufficient task context or as the execution specialist beneath ARM Harness.

## Skill: `arm-coding-worker`

### Description

Use when implementing features, fixing bugs, debugging, refactoring, changing APIs, UI, mobile, databases or infrastructure, upgrading dependencies, fixing builds, or testing and validating software in a repository. Applies to standalone execution and tasks delegated by ARM Harness; excludes purely conceptual engineering discussion.

### Capabilities

- **Adaptive execution loop**: Detect → Classify → Search/Read → Plan → Implement → Validate → Debug → Review
- **Multi-stack support**: JavaScript/TypeScript, React Native/Expo, Python, Go, Rust, Java/Kotlin, .NET, Ruby, PHP, Swift, and mixed-stack monorepos
- **Reference routing**: Loads only applicable references (frontend, backend, mobile, infrastructure, security, etc.)
- **Model profiles**: Configurable for different model capabilities (default, qwen-coder)
- **Harness integration**: Works with ARM Harness for persistent, verifiable workflows

### Installation

```bash
npx skills add armcompany/arm-coding-worker-skill --skill arm-coding-worker
```

Or install all skills from the repo:

```bash
npx skills add armcompany/arm-coding-worker-skill
```

### Usage

Once installed, invoke the skill in your coding agent:

```
Use $arm-coding-worker.

[Your task - e.g., "Add user authentication with JWT tokens to the API"]
```

The skill will:
1. Analyze the repository structure and conventions
2. Detect the project stack and validation commands
3. Plan the smallest coherent change
4. Implement preserving existing architecture
5. Validate with relevant tests and checks
6. Review the diff before completion

### References Included

- `backend-data.md` - API, domain, persistence, migrations, contracts
- `debugging.md` - Systematic debugging approach
- `execution.md` - Complex impact analysis, planning, context preservation
- `frontend.md` - Web UI, Design System, browser behavior
- `harness-integration.md` - Parent task inputs, machine output, checkpoint/resume
- `infrastructure.md` - Infrastructure and delivery configuration
- `mobile.md` - Mobile, native integrations, platform differences
- `project-detection.md` - Project type detection for unfamiliar contexts
- `security.md` - Authentication, permissions, sensitive data, security fixes
- `specialized-work.md` - Shared packages, monorepos, libraries, CLI/desktop
- `validation.md` - Choosing checks and reporting incomplete evidence

### Model Profiles

- `default.md` - Default execution profile
- `qwen-coder.md` - Optimized for Qwen Coder models

### License

MIT