# The Gentleman's Council

A fun opencode agent/command that convenes four council members to deliberate on any topic. Each member has a distinct personality, background, and perspective. The council chair orchestrates deliberation across two rounds and produces a final verdict, persisted to disk.

## Installation

Copy the files into your opencode config directory:

```bash
cp agents/*.md ~/.config/opencode/agents/
```

Then merge the `command` entry from `opencode.json` into your `~/.config/opencode/opencode.json`.

## Usage

```
/council What food should we eat today?
/council What do you think of SpaceX?
/council Is Factorio better than DOTA?
```

## Architecture

- **1 primary agent** (`council-chair`): Facilitates the deliberation, dispatches subagents, reads memorable quotes, synthesizes verdicts
- **4 hidden subagents**: Each with distinct personality, temperature 0.9 for creative flair

## Council Members

| Member | Background | Personality |
|--------|-----------|-------------|
| **The Machine** | Taiwanese SWE | Slow deliberate cadence, nervous energy, DOTA player, foodie, hits on pretty girls, swims for back pain |
| **The Comedian** | Mexican SWE | Jolly joke-cracker, Simpsons/90s TV references, ballroom dancer, Mexican food, positive vibes |
| **The Mitochondrion** | Vietnamese SWE | Quick-witted, PoE player, hosts parties, ping-pong & rock climbing, "mitochondria are active" when hungry |
| **The Panda** | Filipino SWE | Most talented engineer, sarcastic truth-teller, Factorio player, Japanese food lover, permanent eyebags, sloppy dresser |

## Protocol

1. Chair checks past council records for precedent
2. Creates session directory: `docs/the-gentlemans-council/<topic-slug>/<date>/`
3. **Round 1**: Dispatches all 4 members in parallel for opening takes; each writes their own file
4. Reads back memorable quotes verbatim
5. **Round 2**: Dispatches all 4 members for rebuttals (each sees the other 3's full Round 1 takes); each writes their own rebuttal file
6. Reads back memorable quotes from rebuttals
7. Synthesizes a verdict; ties are broken by asking the user
8. Writes `verdict.md`

## File Structure

```
docs/the-gentlemans-council/
  <topic-slug>/
    <date>/
      <timestamp>-r1-the-machine.md
      <timestamp>-r1-the-comedian.md
      <timestamp>-r1-the-mitochondrion.md
      <timestamp>-r1-the-panda.md
      <timestamp>-r2-the-machine.md
      <timestamp>-r2-the-comedian.md
      <timestamp>-r2-the-mitochondrion.md
      <timestamp>-r2-the-panda.md
      <timestamp>-verdict.md
```
