# Data Visualization

Prompts for creating professional, high-performance visualizations in MATLAB with custom styling, animations, and optimized graphics.

## Prompts in this Category

### [Create Custom Multi-Panel Visualizations with Tiledlayout](create-custom-tiledlayout.md)
Design publication-quality multi-panel figures using tiledlayout with optimized performance. Perfect for dashboards, comparison plots, and complex layouts.

**Tags:** `matlab` `visualization` `tiledlayout` `plotting` `performance` `graphics`
**Release:** R2019b+

### [Create High-Performance Animated Plots](create-animated-plots.md)
Create smooth animations by updating plot data efficiently without recreating graphics objects. Includes patterns for real-time data visualization and saving animations.

**Tags:** `matlab` `visualization` `animation` `performance` `drawnow` `graphics`
**Release:** All releases

### [Customize Plot Appearance for Publication Quality](customize-plot-appearance.md)
Transform basic MATLAB plots into publication-ready figures with custom colors, fonts, line styles, and professional styling.

**Tags:** `matlab` `visualization` `styling` `publication` `graphics` `customization`
**Release:** All releases

## Performance Guidelines

All prompts in this category follow MATLAB graphics performance best practices:

- **Update, don't recreate:** Modify XData/YData properties instead of recreating plot objects
- **Modern syntax:** Use dot notation and tiledlayout for better performance
- **Manual limits:** Set axis limits explicitly to prevent auto-calculation overhead
- **Efficient rendering:** Use drawnow limitrate for animations
- **Object consolidation:** Combine data into single objects when possible

## Related Categories

- [Live Scripts & Documentation](../live-scripts-documentation/) - For creating live script visualizations
- [Programming](../programming/) - For optimizing visualization code
- [AI and Statistics](../ai-and-statistics/) - For data analysis visualizations

## Contributing

Have a prompt for data visualization? See [CONTRIBUTING.md](../../CONTRIBUTING.md) for guidelines.
