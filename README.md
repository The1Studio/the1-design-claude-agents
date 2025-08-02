# The1 Designer Claude Agents 🎮

**AI-powered game design tools** that help designers analyze levels, visualize difficulty, and generate new content from screenshots. Built as specialized Claude Code agents for game development teams.

## ⚠️ Important Notice

**This project is experimental and token-intensive.** These agents are designed for game design analysis and can consume significant tokens during complex workflows. Monitor your usage carefully.

## 🚀 Quick Start (3 Minutes)

### Prerequisites
- **Claude Code CLI** installed and authenticated
- **Claude subscription** - required for agent workflows
- Python 3.8+ (for analysis scripts)

### 1. Install the Agents
```bash
git clone https://github.com/The1Studio/the1-designer-claude-agents.git
```

#### Option A: Symlink (Recommended - auto-updates)

**macOS/Linux:**
```bash
ln -sf "$(pwd)/the1-designer-claude-agents" ~/.claude/the1-designer-claude-agents
```

**Windows (PowerShell):**
```powershell
cmd /c mklink /D "$env:USERPROFILE\.claude\the1-designer-claude-agents" "$(Get-Location)\the1-designer-claude-agents"
```

#### Option B: Copy (Static - no auto-updates)
```bash
cp -r the1-designer-claude-agents ~/.claude/
```

### 2. Verify Installation
```bash
claude /agents
# Should show all game design agents
```

### 3. Start Designing
```bash
# Analyze level difficulty
claude "use @agent-level-difficulty-visualizer to analyze my puzzle level"

# Generate levels from screenshots
claude "use @agent-screenshot-analyzer to create new levels from these Candy Crush screenshots"

# Create Python analysis tools
claude "use @agent-python-script-developer to build a difficulty analysis pipeline"
```

## 🎯 What These Agents Do

### Core Capabilities

1. **Level Difficulty Analysis**
   - Visual heatmaps showing difficulty distribution
   - Interactive difficulty curves
   - Bottleneck identification
   - Balancing recommendations

2. **Screenshot-to-Level Generation**
   - Analyze existing game screenshots
   - Extract design patterns and rules
   - Generate new levels in the same style
   - Maintain visual consistency

3. **Game-Specific Analysis**
   - **Puzzle Games**: Move optimization, cognitive load, luck factors
   - **Defense Games**: Wave progression, resource economy, DPS requirements
   - **Platformers**: Jump precision, enemy placement, checkpoint spacing

4. **Python Analysis Tools**
   - Automated batch analysis
   - Statistical modeling
   - Computer vision for screenshots
   - Interactive Jupyter notebooks

## 👥 Meet Your Game Design AI Team

### 🎭 Orchestrators (1 agent)
- **[Game Design Orchestrator](agents/orchestrators/game-design-orchestrator.md)** - Coordinates all design tasks and analysis workflows

### 🎮 Core Design Agents (3 agents)
- **[Level Difficulty Visualizer](agents/core/level-difficulty-visualizer.md)** - Creates interactive difficulty visualizations
- **[Screenshot Analyzer](agents/core/screenshot-analyzer.md)** - Extracts patterns from game screenshots
- **[Pattern Learning Agent](agents/core/pattern-learning-agent.md)** - Learns design rules from examples

### 🎯 Specialized Game Agents (2 agents)
- **[Puzzle Difficulty Analyzer](agents/specialized/puzzle/puzzle-difficulty-analyzer.md)** - Match-3, sliding puzzles, logic games
- **[Defense Game Wave Analyzer](agents/specialized/defense/defense-game-wave-analyzer.md)** - Tower defense, wave survival

### 🐍 Python Analysis Agents (4 agents)
- **[Python Script Developer](agents/python/python-script-developer.md)** - Creates analysis scripts and automation
- **[OpenCV Vision Expert](agents/python/opencv-vision-expert.md)** - Computer vision for screenshots
- **[Data Science Analyst](agents/python/data-science-analyst.md)** - Statistical analysis and ML
- **[Jupyter Notebook Creator](agents/python/jupyter-notebook-creator.md)** - Interactive analysis tools

### 🌐 Universal Tools (4 agents)
- **[Interactive UI Builder](agents/universal/interactive-ui-builder.md)** - HTML/JS visualization interfaces
- **[Level Data Parser](agents/universal/level-data-parser.md)** - Handles any level format
- **[Visualization Renderer](agents/universal/visualization-renderer.md)** - Charts, heatmaps, graphs
- **[Export Format Converter](agents/universal/export-format-converter.md)** - Unity, Cocos, JSON outputs

**Total: 15 specialized agents** for game design and analysis!

## 📈 Example Workflows

### Analyze Level Difficulty
```bash
claude "I have a platformer level JSON file. Create an interactive difficulty visualization showing bottlenecks and recommendations"
```

### Generate Levels from Screenshots
```bash
claude "I have 5 screenshots from Candy Crush. Learn the patterns and generate 10 new levels with similar difficulty progression"
```

### Create Analysis Pipeline
```bash
claude "Build a Python script that analyzes all levels in my game and generates a difficulty report with visualizations"
```

### Interactive Design Tool
```bash
claude "Create an HTML tool where I can drag and drop level files to see instant difficulty analysis with heatmaps"
```

## 🔥 Key Features

- **Visual-First Design** - Everything outputs as interactive visualizations
- **Engine Agnostic** - Works with Unity, Cocos, Godot, or custom engines
- **Designer Friendly** - No coding required for basic usage
- **Export Anywhere** - JSON, CSV, HTML, or engine-specific formats
- **Real-Time Preview** - See changes instantly as you adjust parameters

## 📚 Learn More

- [Creating Custom Agents](docs/creating-agents.md) - Build specialized agents for your games
- [Best Practices](docs/best-practices.md) - Get the most from your AI team
- [Integration Guide](docs/integration-guide.md) - Connect with your game engine

## 💬 Join The Community

- ⭐ **Star this repo** to show support
- 🐛 [Report issues](https://github.com/The1Studio/the1-designer-claude-agents/issues)
- 💡 [Share ideas](https://github.com/The1Studio/the1-designer-claude-agents/discussions)

## 📄 License

MIT License - Use freely in your game projects!

---

<p align="center">
  <strong>Transform game design with AI-powered analysis and generation tools</strong><br>
  <em>From screenshots to playable levels in minutes.</em>
</p>

<p align="center">
  <a href="https://github.com/The1Studio/the1-designer-claude-agents">GitHub</a> •
  <a href="docs/creating-agents.md">Documentation</a> •
  <a href="https://github.com/The1Studio/the1-designer-claude-agents/discussions">Community</a>
</p>