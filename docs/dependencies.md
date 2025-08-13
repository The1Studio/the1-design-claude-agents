# Dependencies

## Context7 MCP (Optional)

Some agents reference Context7 MCP for fetching up-to-date design and development documentation. While not required (agents will use WebFetch as fallback), Context7 provides better documentation access.

### Installation

1. Install Context7 MCP server:
```bash
npm install -g @context7/mcp-server
```

2. Configure in Claude's MCP settings:
```json
{
  "mcpServers": {
    "context7": {
      "command": "context7-mcp",
      "args": []
    }
  }
}
```

3. Restart Claude Code to activate

### Benefits
- Faster design documentation retrieval
- Better structured responses for visual analysis
- Cached documentation access for design tools

Without Context7, agents automatically use WebFetch to fetch documentation from official design tool websites.

## Design Analysis Dependencies

### Required Python Libraries
- **OpenCV**: For computer vision and image processing
- **NumPy**: For numerical operations on image data
- **Matplotlib**: For data visualization and plotting
- **Pillow (PIL)**: For image manipulation and processing
- **scikit-image**: For advanced image processing algorithms

### Installation
```bash
pip install opencv-python numpy matplotlib pillow scikit-image
```

### Optional Data Science Tools
- **Pandas**: For data analysis and manipulation
- **Jupyter**: For interactive data analysis notebooks
- **Seaborn**: For statistical data visualization
- **Plotly**: For interactive visualizations

### Recommended Development Tools
- **Visual Studio Code**: With Python and Jupyter extensions
- **PyCharm**: Professional Python IDE
- **Git**: For version control of analysis scripts

### Image Format Support
The agents can work with common image formats:
- PNG, JPG, JPEG
- GIF (static analysis)
- BMP, TIFF
- WebP
- SVG (basic support)

### Performance Considerations
- Large image files may require additional memory
- Complex visual analysis may benefit from GPU acceleration
- Consider image compression for faster processing

### Optional GPU Acceleration
For advanced image processing:
- **CUDA** (NVIDIA GPUs)
- **OpenCL** (Cross-platform GPU computing)
- **TensorFlow** or **PyTorch** for machine learning-based analysis