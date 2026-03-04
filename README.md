# Analysis Plugin for Claude Code

A structured thinking framework for analysis and decision making, grounded in intelligence analysis methodologies and strategic consulting practices.

## Commands

| Command | Purpose |
|---------|---------|
| `analysis:analyze` | Plan your analysis: suggests personas, identifies the key question, assesses complexity, recommends command sequence |
| `analysis:research` | Gather external context, industry trends, evidence base. Runs as a subagent to keep main context clean. |
| `analysis:evaluate` | Five perspectives with assumption tracking: Informed, Steelman, Skeptic, Practical, Contrarian |
| `analysis:critique` | Adversarial stress test: severity rated flaws, pre mortem, cross domain concerns |
| `analysis:synthesize` | Structured output: summary, critique integration, recommendation with confidence, categorized open questions |
| `analysis:decide` | Decision landscape with viable paths, type detection, user checkpoint, structured decision record |
| `analysis:quick` | Lightweight mode: compressed analysis in a single pass under 500 words |
| `analysis:test` | Validate the framework: runs three scenarios and scores output quality |

## Usage

### Full Framework

For complex, high stakes, or ambiguous decisions:

```
/analysis:analyze [your topic]
```

This will identify the key question, suggest personas, and output the commands to run:

```
/analysis:research [topic]. Approach as a [persona].
/analysis:evaluate [topic]. Approach as a [persona].
/analysis:critique [topic]. Approach as a [persona].
/analysis:synthesize
/analysis:decide
```

The analyze step also detects when adjacent domains are relevant and adds cross domain flags to the critique command automatically.

### Quick Mode

For straightforward, reversible, or time constrained decisions:

```
/analysis:quick [your topic]. Approach as a [persona].
```

### Skipping Steps

You can skip steps or run them out of order. The framework is designed for flexibility:
- Run just research and evaluate if you want evidence and perspectives without the full pipeline
- Jump straight to decide if you have already done your own analysis
- Use critique standalone to stress test any idea

### Testing the Framework

After making changes to any skill, validate with:

```
/analysis:test
```

This runs three predefined scenarios covering strategic, people, and technical decisions, then scores each step against a quality rubric.

## Personas

Each command supports a persona that layers domain expertise onto the analysis:

- "Approach as a financial analyst"
- "Approach as a systems architect"
- "Approach as a product manager"
- "Approach as a cognitive systems designer"

The persona affects what evidence matters, what concerns arise, and how recommendations are framed. The analyze step generates rich personas with specific experience, context, and formative events rather than generic role titles.

## Architecture

### Research Subagent

The research step runs in a forked context via the `analysis-researcher` agent. This keeps high volume web search output out of the main conversation window. Research output is structured with key findings, evidence quality assessment, source citations, and identified gaps.

### Decision Type Detection

The decide step detects three decision types and adapts its output format:
- **Clear Choice**: For binary or technical decisions with strong evidence
- **Phased Approach**: For decisions with significant uncertainty or multiple stages
- **Navigational**: For people, coaching, and relationship decisions where principles matter more than rigid actions

### Framework Validation

The test skill runs the full pipeline against three embedded scenarios and scores output quality across multiple dimensions per step. This provides a repeatable way to validate changes.

## Installation

```bash
claude plugins add github:hartyquinn/claude-plugin-analysis
```

## License

MIT
