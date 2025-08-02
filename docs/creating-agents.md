# Creating Game Design Agents

Learn how to create specialized agents for game design and analysis tasks.

## Quick Start Template

```yaml
---
name: your-game-agent
description: |
  One-line description of what this agent does for game designers.
  
  Examples:
  - <example>
    Context: When to use this agent
    user: "Analyze my tower defense waves"
    assistant: "I'll use the your-game-agent to analyze wave progression"
    <commentary>
    Why this agent was selected
    </commentary>
  </example>
tools: Read, Write, Edit, Bash  # Optional - inherits all if omitted
---

You are a game design specialist focusing on [specific area].

## Core Expertise
- [Specific game design skill]
- [Analysis capability]
- [Visualization type]

## Task Approach
1. Parse game data
2. Analyze specific metrics
3. Generate visualizations
4. Provide recommendations

## Output Format
Always return both designer-friendly and developer-ready formats:
```json
{
  "designer_summary": "Clear insights",
  "visualizations": ["heatmap.html", "difficulty_curve.png"],
  "developer_data": { /* raw metrics */ },
  "recommendations": ["specific improvements"]
}
```
```

## Game Design Agent Patterns

### Analysis Agents
Focus on extracting insights from game data:

```yaml
name: rpg-balance-analyzer
description: |
  Analyzes RPG character stats, item values, and progression curves.
  MUST BE USED for balancing RPG economies and combat systems.
```

### Visualization Agents
Create interactive visual tools:

```yaml
name: player-path-visualizer
description: |
  Creates heatmaps showing player movement patterns and bottlenecks.
  MUST BE USED for optimizing level flow and identifying problem areas.
```

### Generation Agents
Create new content based on rules:

```yaml
name: procedural-level-generator
description: |
  Generates levels using learned patterns and design constraints.
  MUST BE USED for creating level variations and procedural content.
```

## Best Practices for Game Agents

### 1. Understand the Designer's Needs
- Designers want visual feedback, not raw numbers
- Provide actionable recommendations
- Support iterative workflows

### 2. Game-Specific Knowledge
```javascript
// Good: Game-aware metrics
const puzzleMetrics = {
  minMoves: 15,
  luckFactor: 0.2,
  cognitiveLoad: "medium"
};

// Bad: Generic metrics
const metrics = {
  score: 75,
  difficulty: 6
};
```

### 3. Interactive Output
Always generate interactive HTML when possible:

```html
<div class="interactive-analysis">
  <canvas id="heatmap"></canvas>
  <div class="controls">
    <input type="range" onchange="updateDifficulty(this.value)">
  </div>
</div>
```

### 4. Multiple Export Formats
```javascript
function exportResults(data) {
  return {
    json: exportJSON(data),
    unity: exportUnityFormat(data),
    cocos: exportCocosFormat(data),
    csv: exportCSV(data),
    html: exportInteractiveHTML(data)
  };
}
```

## Testing Your Game Agent

### 1. Sample Data
Always test with various game types:
- Simple tutorial levels
- Complex end-game content  
- Edge cases (empty levels, massive levels)

### 2. Visualization Quality
- Check readability at different scales
- Verify color choices for accessibility
- Test interactivity on touch devices

### 3. Performance
- Handle large level files (1000+ elements)
- Optimize visualization rendering
- Cache computed metrics

## Common Game Agent Types

### Difficulty Analyzers
```yaml
name: platformer-difficulty-analyzer
description: |
  Analyzes jump distances, enemy placement, and checkpoint spacing.
  Calculates precision requirements and reaction time windows.
```

### Economy Balancers
```yaml
name: game-economy-balancer
description: |
  Balances in-game currencies, item prices, and reward rates.
  Prevents inflation and ensures progression feels rewarding.
```

### Player Behavior Analyzers
```yaml
name: player-retention-analyzer
description: |
  Analyzes player drop-off points and engagement metrics.
  Identifies frustration points and suggests improvements.
```

## Integration Examples

### With Unity
```csharp
[CreateAssetMenu(fileName = "LevelAnalysis", menuName = "GameDesign/Analysis")]
public class LevelAnalysisData : ScriptableObject
{
    public float difficultyScore;
    public DifficultyMetrics metrics;
    public List<string> recommendations;
}
```

### With Web Tools
```javascript
// Real-time preview integration
class DesignToolBridge {
  constructor() {
    this.socket = new WebSocket('ws://localhost:8080');
  }
  
  updateLevel(changes) {
    this.socket.send(JSON.stringify({
      type: 'level_update',
      changes: changes
    }));
  }
}
```

## Next Steps

1. Browse existing agents in [agents/](../agents/) for examples
2. Start with the game agent template above
3. Focus on one specific game design problem
4. Test with real game data
5. Share your agent with the community!