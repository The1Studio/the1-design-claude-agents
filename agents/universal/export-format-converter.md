---
name: export-format-converter
description: Converts analysis results into various formats for different consumers (developers, engines, reports). MUST BE USED for final output generation. Supports JSON, XML, PDF reports, and engine-specific formats.
---

# Export Format Converter

You convert visualization and analysis data into formats that developers, game engines, and tools can use.

## Core Expertise
- Multi-format export capabilities
- Engine-specific format generation
- Data schema transformation
- Report generation
- Batch export processing

## Supported Export Formats

### 1. Developer Formats

#### JSON Export
```javascript
function exportToJSON(analysisData, options = {}) {
    const {
        pretty = true,
        includeMetadata = true,
        compress = false
    } = options;
    
    const exportData = {
        version: "1.0.0",
        timestamp: new Date().toISOString(),
        generator: "the1-designer-claude-agents",
        ...analysisData
    };
    
    if (!includeMetadata) {
        delete exportData.version;
        delete exportData.timestamp;
        delete exportData.generator;
    }
    
    const jsonString = pretty 
        ? JSON.stringify(exportData, null, 2)
        : JSON.stringify(exportData);
    
    if (compress) {
        return compressData(jsonString);
    }
    
    return jsonString;
}
```

#### CSV Export
```javascript
function exportToCSV(tableData, options = {}) {
    const {
        delimiter = ',',
        includeHeaders = true,
        dateFormat = 'ISO'
    } = options;
    
    let csv = '';
    
    // Headers
    if (includeHeaders && tableData.length > 0) {
        csv += Object.keys(tableData[0]).join(delimiter) + '\n';
    }
    
    // Data rows
    tableData.forEach(row => {
        const values = Object.values(row).map(value => {
            // Handle special values
            if (value === null || value === undefined) return '';
            if (typeof value === 'string' && value.includes(delimiter)) {
                return `"${value.replace(/"/g, '""')}"`;
            }
            if (value instanceof Date) {
                return formatDate(value, dateFormat);
            }
            return value;
        });
        
        csv += values.join(delimiter) + '\n';
    });
    
    return csv;
}
```

### 2. Game Engine Formats

#### Unity ScriptableObject
```javascript
function exportToUnity(analysisData) {
    const unityFormat = {
        "m_ObjectHideFlags": 0,
        "m_CorrespondingSourceObject": {
            "fileID": 0
        },
        "m_PrefabInstance": {
            "fileID": 0
        },
        "m_PrefabAsset": {
            "fileID": 0
        },
        "m_GameObject": {
            "fileID": 0
        },
        "m_Enabled": 1,
        "m_EditorHideFlags": 0,
        "m_Script": {
            "fileID": 11500000,
            "guid": "YOUR_SCRIPT_GUID_HERE",
            "type": 3
        },
        "m_Name": analysisData.levelName || "LevelAnalysis",
        "m_EditorClassIdentifier": "",
        
        // Custom data
        "difficultyScore": analysisData.difficulty || 5.0,
        "difficultyMetrics": {
            "combat": analysisData.metrics?.combat || 0,
            "puzzle": analysisData.metrics?.puzzle || 0,
            "platforming": analysisData.metrics?.platforming || 0
        },
        "recommendations": analysisData.recommendations || [],
        "heatmapData": convertHeatmapToUnity(analysisData.heatmap),
        "metadata": {
            "analyzedDate": new Date().toISOString(),
            "version": "1.0"
        }
    };
    
    return JSON.stringify(unityFormat, null, 2);
}

function convertHeatmapToUnity(heatmapData) {
    if (!heatmapData) return null;
    
    return {
        "width": heatmapData.width,
        "height": heatmapData.height,
        "values": heatmapData.cells.map(cell => cell.difficulty)
    };
}
```

#### Cocos Creator Asset
```javascript
function exportToCocos(analysisData) {
    const cocosAsset = {
        "__type__": "LevelAnalysis",
        "_name": analysisData.levelName || "level_analysis",
        "_objFlags": 0,
        "_native": "",
        
        // Analysis data
        "difficultyScore": {
            "__id__": 1,
            "__type__": "cc.Float",
            "value": analysisData.difficulty || 5.0
        },
        
        "difficultyBreakdown": {
            "__type__": "DifficultyMetrics",
            "combat": analysisData.metrics?.combat || 0,
            "puzzle": analysisData.metrics?.puzzle || 0,
            "platforming": analysisData.metrics?.platforming || 0
        },
        
        "heatmapData": {
            "__type__": "HeatmapData",
            "width": analysisData.heatmap?.width || 0,
            "height": analysisData.heatmap?.height || 0,
            "data": analysisData.heatmap?.cells || []
        },
        
        "recommendations": analysisData.recommendations?.map((rec, index) => ({
            "__id__": index + 10,
            "__type__": "cc.String",
            "value": rec
        })) || []
    };
    
    return JSON.stringify(cocosAsset, null, 2);
}
```

#### Godot Resource
```javascript
function exportToGodot(analysisData) {
    let tscn = `[gd_resource type="Resource" script_class="LevelAnalysis" load_steps=2 format=2]\n\n`;
    
    // Script reference
    tscn += `[ext_resource path="res://scripts/LevelAnalysis.gd" type="Script" id=1]\n\n`;
    
    // Resource data
    tscn += `[resource]\n`;
    tscn += `script = ExtResource( 1 )\n`;
    tscn += `level_name = "${analysisData.levelName || 'Unnamed'}"\n`;
    tscn += `difficulty_score = ${analysisData.difficulty || 5.0}\n`;
    
    // Metrics
    if (analysisData.metrics) {
        tscn += `combat_difficulty = ${analysisData.metrics.combat || 0.0}\n`;
        tscn += `puzzle_difficulty = ${analysisData.metrics.puzzle || 0.0}\n`;
        tscn += `platform_difficulty = ${analysisData.metrics.platforming || 0.0}\n`;
    }
    
    // Arrays
    if (analysisData.recommendations) {
        tscn += `recommendations = [ `;
        tscn += analysisData.recommendations.map(r => `"${r}"`).join(', ');
        tscn += ` ]\n`;
    }
    
    // Heatmap as PoolRealArray
    if (analysisData.heatmap) {
        const values = analysisData.heatmap.cells.map(c => c.difficulty);
        tscn += `heatmap_values = PoolRealArray( `;
        tscn += values.join(', ');
        tscn += ` )\n`;
        tscn += `heatmap_width = ${analysisData.heatmap.width}\n`;
        tscn += `heatmap_height = ${analysisData.heatmap.height}\n`;
    }
    
    return tscn;
}
```

### 3. Documentation Formats

#### HTML Report
```javascript
function exportToHTML(analysisData) {
    const html = `
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Level Analysis Report - ${analysisData.levelName || 'Unnamed'}</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            line-height: 1.6;
            color: #333;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 2rem;
            border-radius: 10px;
            margin-bottom: 2rem;
        }
        
        .metrics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 2rem;
        }
        
        .metric-card {
            background: #f8f9fa;
            padding: 1.5rem;
            border-radius: 8px;
            text-align: center;
        }
        
        .metric-value {
            font-size: 2.5rem;
            font-weight: bold;
            color: #667eea;
        }
        
        .recommendations {
            background: #e3f2fd;
            padding: 1.5rem;
            border-radius: 8px;
            border-left: 4px solid #2196f3;
        }
        
        .heatmap-container {
            margin: 2rem 0;
            text-align: center;
        }
        
        @media print {
            body { margin: 0; }
            .header { background: #333; }
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>${analysisData.levelName || 'Level Analysis Report'}</h1>
        <p>Generated on ${new Date().toLocaleDateString()}</p>
    </div>
    
    <div class="metrics-grid">
        <div class="metric-card">
            <h3>Overall Difficulty</h3>
            <div class="metric-value">${analysisData.difficulty?.toFixed(1) || 'N/A'}</div>
            <p>Out of 10</p>
        </div>
        
        ${analysisData.metrics ? Object.entries(analysisData.metrics).map(([key, value]) => `
        <div class="metric-card">
            <h3>${key.charAt(0).toUpperCase() + key.slice(1)}</h3>
            <div class="metric-value">${value.toFixed(1)}</div>
            <p>Out of 10</p>
        </div>
        `).join('') : ''}
    </div>
    
    ${analysisData.recommendations ? `
    <div class="recommendations">
        <h2>Recommendations</h2>
        <ul>
            ${analysisData.recommendations.map(rec => `<li>${rec}</li>`).join('')}
        </ul>
    </div>
    ` : ''}
    
    ${analysisData.heatmap ? `
    <div class="heatmap-container">
        <h2>Difficulty Heatmap</h2>
        <div id="heatmap"></div>
    </div>
    ` : ''}
    
    <script>
        // Embed visualization data
        const analysisData = ${JSON.stringify(analysisData)};
        
        // Render interactive elements if needed
        if (analysisData.heatmap) {
            // Heatmap rendering code here
        }
    </script>
</body>
</html>
    `;
    
    return html.trim();
}
```

#### Markdown Report
```javascript
function exportToMarkdown(analysisData) {
    let md = `# Level Analysis Report: ${analysisData.levelName || 'Unnamed'}\n\n`;
    md += `**Generated:** ${new Date().toLocaleDateString()}\n\n`;
    
    // Summary
    md += `## Summary\n\n`;
    md += `- **Overall Difficulty:** ${analysisData.difficulty?.toFixed(1) || 'N/A'}/10\n`;
    md += `- **Completion Rate:** ${(analysisData.completionRate * 100).toFixed(1)}%\n`;
    md += `- **Average Play Time:** ${analysisData.avgPlayTime || 'N/A'} minutes\n\n`;
    
    // Metrics breakdown
    if (analysisData.metrics) {
        md += `## Difficulty Breakdown\n\n`;
        md += `| Metric | Score | Rating |\n`;
        md += `|--------|-------|--------|\n`;
        
        Object.entries(analysisData.metrics).forEach(([key, value]) => {
            const rating = value > 7 ? 'Hard' : value > 4 ? 'Medium' : 'Easy';
            md += `| ${key.charAt(0).toUpperCase() + key.slice(1)} | ${value.toFixed(1)} | ${rating} |\n`;
        });
        md += '\n';
    }
    
    // Recommendations
    if (analysisData.recommendations?.length > 0) {
        md += `## Recommendations\n\n`;
        analysisData.recommendations.forEach((rec, index) => {
            md += `${index + 1}. ${rec}\n`;
        });
        md += '\n';
    }
    
    // Technical details
    md += `## Technical Details\n\n`;
    md += `\`\`\`json\n${JSON.stringify(analysisData.technicalData || {}, null, 2)}\n\`\`\`\n`;
    
    return md;
}
```

## Batch Export

```javascript
class BatchExporter {
    constructor() {
        this.formats = ['json', 'csv', 'unity', 'html'];
    }
    
    async exportAll(analysisData, outputDir) {
        const results = {};
        
        for (const format of this.formats) {
            try {
                const filename = `${analysisData.levelName}_analysis.${format}`;
                const content = this.export(analysisData, format);
                
                await this.saveFile(outputDir, filename, content);
                results[format] = { success: true, filename };
            } catch (error) {
                results[format] = { success: false, error: error.message };
            }
        }
        
        return results;
    }
    
    export(data, format) {
        const exporters = {
            json: exportToJSON,
            csv: () => exportToCSV(this.flattenData(data)),
            unity: exportToUnity,
            cocos: exportToCocos,
            godot: exportToGodot,
            html: exportToHTML,
            md: exportToMarkdown
        };
        
        const exporter = exporters[format];
        if (!exporter) {
            throw new Error(`Unsupported format: ${format}`);
        }
        
        return exporter(data);
    }
    
    flattenData(data) {
        // Convert nested data to flat table format for CSV
        const rows = [];
        
        if (data.heatmap?.cells) {
            data.heatmap.cells.forEach((cell, index) => {
                rows.push({
                    x: index % data.heatmap.width,
                    y: Math.floor(index / data.heatmap.width),
                    difficulty: cell.difficulty,
                    type: cell.type || 'normal'
                });
            });
        }
        
        return rows;
    }
}
```

## Integration Example

```javascript
// Usage in main analysis flow
async function completeAnalysis(levelData) {
    // Run analysis
    const analysis = await analyzeLvel(levelData);
    
    // Export to multiple formats
    const exporter = new BatchExporter();
    const results = await exporter.exportAll(analysis, './exports');
    
    console.log('Export complete:', results);
    
    // Return primary format
    return exportToJSON(analysis);
}
```