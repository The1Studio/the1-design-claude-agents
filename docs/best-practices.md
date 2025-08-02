# Best Practices for Game Design Agents

> **Goal** – Create effective, designer-friendly agents that provide actionable insights and beautiful visualizations for game development.

## 1. Designer-First Thinking

| Principle | Do | Don't |
|-----------|----|----|
| **Visual Output** | Interactive heatmaps, graphs | Raw JSON dumps |
| **Language** | "Difficulty spike at checkpoint 3" | "Metrics indicate 0.73 failure rate" |
| **Recommendations** | "Add 2 health pickups before boss" | "Increase resource availability by 15%" |
| **Interactivity** | Click to explore, drag to adjust | Static reports |

## 2. Game-Aware Analysis

### Understand Game Mechanics
```python
# Good: Game-specific metrics
def analyze_puzzle_level(level):
    return {
        "move_efficiency": calculate_minimum_moves(level),
        "luck_dependency": measure_randomness_impact(level),
        "cognitive_load": assess_mental_complexity(level),
        "teaching_effectiveness": check_mechanic_introduction(level)
    }

# Bad: Generic metrics
def analyze_level(level):
    return {"score": 75, "difficulty": "hard"}
```

### Genre-Specific Patterns
- **Puzzle Games**: Focus on solution paths, cognitive load
- **Platformers**: Analyze jump precision, reaction windows
- **Tower Defense**: Track DPS requirements, economy balance
- **RPGs**: Balance progression curves, loot distribution

## 3. Interactive Visualizations

### Always Include Interactivity
```javascript
// Interactive heatmap example
function createInteractiveHeatmap(data) {
    const cells = data.map((value, index) => ({
        value,
        onClick: () => showDetailedAnalysis(index),
        onHover: () => showTooltip(index),
        color: difficultyToColor(value)
    }));
    
    return renderHeatmap(cells);
}
```

### Real-Time Updates
```javascript
// Enable live preview
class LivePreview {
    constructor(updateCallback) {
        this.callback = updateCallback;
        this.throttle = 16; // 60fps
    }
    
    update(changes) {
        requestAnimationFrame(() => {
            this.callback(changes);
        });
    }
}
```

## 4. Data Processing Best Practices

### Handle Multiple Formats
```python
class UniversalParser:
    def parse(self, file_path):
        ext = file_path.suffix.lower()
        
        parsers = {
            '.json': self.parse_json,
            '.xml': self.parse_xml,
            '.csv': self.parse_csv,
            '.tmx': self.parse_tiled
        }
        
        parser = parsers.get(ext, self.parse_text)
        return parser(file_path)
```

### Graceful Error Handling
```python
def analyze_level_safe(level_data):
    try:
        return analyze_level(level_data)
    except KeyError as e:
        return {
            "error": f"Missing required field: {e}",
            "suggestion": "Check level format matches schema",
            "partial_results": analyze_what_we_can(level_data)
        }
```

## 5. Performance Optimization

### Large Dataset Handling
```python
# Process in chunks for large levels
def analyze_large_level(level_data, chunk_size=1000):
    results = []
    
    for i in range(0, len(level_data), chunk_size):
        chunk = level_data[i:i + chunk_size]
        results.append(process_chunk(chunk))
        
        # Update progress
        yield {"progress": i / len(level_data)}
    
    return combine_results(results)
```

### Caching Expensive Computations
```javascript
const cache = new Map();

function expensiveAnalysis(data) {
    const key = hashData(data);
    
    if (cache.has(key)) {
        return cache.get(key);
    }
    
    const result = performAnalysis(data);
    cache.set(key, result);
    
    return result;
}
```

## 6. Export Format Guidelines

### Multiple Output Options
```python
def export_analysis(results, format='json'):
    exporters = {
        'json': lambda r: json.dumps(r, indent=2),
        'csv': lambda r: results_to_csv(r),
        'unity': lambda r: create_unity_scriptable_object(r),
        'html': lambda r: generate_interactive_report(r),
        'pdf': lambda r: create_pdf_report(r)
    }
    
    return exporters[format](results)
```

### Engine-Specific Formats
```javascript
// Unity ScriptableObject format
function toUnityFormat(analysis) {
    return {
        "m_ObjectHideFlags": 0,
        "m_Script": "{fileID: 11500000, guid: YOUR_GUID}",
        "m_Name": "LevelAnalysis",
        "difficultyScore": analysis.difficulty,
        "recommendations": analysis.recommendations
    };
}
```

## 7. Documentation Standards

### Clear Agent Descriptions
```yaml
---
name: wave-survival-analyzer
description: |
  Analyzes wave-based survival games for difficulty progression and resource balance.
  MUST BE USED when balancing enemy waves, resource drops, and upgrade costs.
  Provides interactive timeline visualization of difficulty spikes.
---
```

### Helpful Examples
Always include concrete examples:
```python
"""
Example usage:
    analyzer = WaveSurvivalAnalyzer()
    results = analyzer.analyze("levels/survival_map_01.json")
    
    # Access specific metrics
    print(f"Wave 10 intensity: {results.waves[10].intensity}")
    print(f"Resource balance: {results.economy.balance_score}")
    
    # Generate visualization
    analyzer.create_timeline_chart(results, "wave_difficulty.html")
"""
```

## 8. Testing Checklist

- ✅ Works with minimal data (empty level)
- ✅ Handles large datasets (1000+ elements)
- ✅ Produces valid visualizations
- ✅ Exports to all promised formats
- ✅ Provides helpful error messages
- ✅ Runs in under 5 seconds for typical data
- ✅ Interactive elements work on mobile
- ✅ Colors are accessible (colorblind-safe)

## 9. Common Pitfalls to Avoid

### Don't Overwhelm with Data
```python
# Bad: Information overload
return {
    "metric1": 0.7823,
    "metric2": 0.1234,
    "metric3": 0.9876,
    # ... 50 more metrics
}

# Good: Focused insights
return {
    "overall_difficulty": "Medium-Hard",
    "key_issues": [
        "Difficulty spike at 30% progression",
        "Resource scarcity in mid-game"
    ],
    "quick_fixes": [
        "Add checkpoint before boss",
        "Increase coin drops by 20%"
    ]
}
```

### Don't Ignore Context
- Consider player skill levels
- Account for different playstyles  
- Remember platform differences (mobile vs PC)
- Respect genre conventions

## 10. Future-Proofing

### Extensible Design
```python
class BaseAnalyzer:
    def analyze(self, data):
        results = {}
        
        # Run all registered analyzers
        for analyzer in self.analyzers:
            results.update(analyzer(data))
            
        return results
    
    def register_analyzer(self, analyzer):
        self.analyzers.append(analyzer)
```

### Version Your Outputs
```json
{
  "version": "1.2.0",
  "analyzer": "puzzle-difficulty-analyzer",
  "timestamp": "2024-01-15T10:30:00Z",
  "results": { /* ... */ }
}
```

## Quick Reference Card

```python
# Every game design agent should:
1. Output interactive visualizations
2. Speak designer language  
3. Provide actionable recommendations
4. Support multiple export formats
5. Handle errors gracefully
6. Process data efficiently
7. Include helpful examples
8. Test with real game data
```

Remember: **Great game design agents make designers more creative, not just more informed.**