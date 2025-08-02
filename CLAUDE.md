# CLAUDE.md

This file provides guidance to Claude Code when working with The1 Designer Claude Agents repository.

## Project Overview

This is The1 Designer Claude Agents - a collection of specialized AI agents that help game designers analyze levels, visualize difficulty, and generate content from screenshots. The agents work together to provide comprehensive game design tools without requiring coding knowledge from designers.

## Working with Game Design Agents

When creating or modifying agents:
1. Focus on visual output - designers prefer interactive visualizations over raw data
2. Support multiple game genres (puzzle, defense, platformer, etc.)
3. Export to common formats (JSON, Unity, Cocos, HTML)
4. Keep tools simple and intuitive for non-programmers

## Agent Organization

### Agent Categories
The project follows this structure:

1. **Orchestrators** (`agents/orchestrators/`)
   - `game-design-orchestrator`: Coordinates all design tasks

2. **Core Agents** (`agents/core/`)
   - Essential tools for analysis and visualization
   - Work across all game types

3. **Specialized Agents** (`agents/specialized/`)
   - Game-type specific analyzers
   - Subdirectories: puzzle/, defense/, platformer/

4. **Python Agents** (`agents/python/`)
   - Script development and data analysis
   - Computer vision and ML tools

5. **Universal Agents** (`agents/universal/`)
   - UI building, data parsing, export tools
   - Framework-agnostic helpers

## Key Design Principles

### Visual-First Approach
- Always generate interactive HTML visualizations
- Use colors, charts, and heatmaps
- Make data exploration intuitive
- Support drag-and-drop interfaces

### Game-Aware Analysis
- Understand different game mechanics
- Provide genre-specific metrics
- Suggest improvements based on game type
- Learn from existing successful games

### Designer-Friendly Output
```json
{
  "designer_view": {
    "summary": "human-readable insights",
    "recommendations": ["clear action items"],
    "visual_preview": "embedded visualization"
  },
  "developer_data": {
    "raw_metrics": {},
    "export_formats": ["json", "unity", "cocos"]
  }
}
```

## Common Workflows

### Level Difficulty Analysis
```
1. Parse level data → level-data-parser
2. Analyze difficulty → puzzle-difficulty-analyzer OR defense-game-wave-analyzer
3. Generate visualizations → visualization-renderer
4. Build interface → interactive-ui-builder
5. Export results → export-format-converter
```

### Screenshot to Level Generation
```
1. Analyze screenshots → screenshot-analyzer
2. Learn patterns → pattern-learning-agent
3. Generate levels → level-generator
4. Validate playability → constraint-validator
5. Match visual style → visual-style-matcher
```

### Python Analysis Pipeline
```
1. Create scripts → python-script-developer
2. Process images → opencv-vision-expert
3. Analyze data → data-science-analyst
4. Build notebooks → jupyter-notebook-creator
```

## Integration with Game Engines

### Unity
- Export as ScriptableObjects
- Generate C# data classes
- Create Unity Editor tools

### Cocos Creator
- Export as Cocos assets
- Generate TypeScript interfaces
- Create Cocos extensions

### Generic Export
- Standard JSON schema
- CSV for spreadsheets
- HTML for documentation

## Best Practices

1. **Always Test Visualizations**
   - Ensure they work in all browsers
   - Test on mobile devices
   - Verify data accuracy

2. **Provide Examples**
   - Include sample level files
   - Show before/after comparisons
   - Demonstrate all features

3. **Error Handling**
   - Gracefully handle unknown formats
   - Provide helpful error messages
   - Suggest corrections

4. **Performance**
   - Optimize for large level files
   - Use efficient algorithms
   - Cache processed data

## Important Files

- `README.md`: User-facing documentation
- `CLAUDE.md`: This file - agent guidance
- `agents/`: All agent definitions
- `docs/`: Additional documentation
- `examples/`: Sample files and demos

## Agent Communication

Since sub-agents cannot invoke each other directly:
- Return structured data for the main agent to parse
- Include clear next steps in responses
- Provide all necessary context for follow-up tasks
- Use consistent data schemas across agents