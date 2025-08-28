# Command-Line Tools

The following tools can be used from the command-line to perform tasks on behalf of the user.

## `magick` - ImageMagick Image Conversion

Use ImageMagick to convert images from one format to another.

```bash
Usage: magick [options ...] file [ [options ...] file ...] [options ...] file
```

### Key Parameters

1. **Multi-size support**: `-define icon:auto-resize=` accepts comma-separated pixel dimensions (multiple sizes recommended)
2. **Transparency preservation**: Add `-transparent COLOR` to remove background
3. **SVG scaling**: For vector inputs, specify base resolution

### Common Use Cases

#### Convert to Favicon (ICO format)
```bash
# Basic conversion with multiple sizes
magick INPUT.(svg|png) -define icon:auto-resize=16,24,32,48,64,128,256 OUTPUT.ico

# PNG to ICO
magick logo.png -define icon:auto-resize=16,32,48,64 favicon.ico

# SVG to ICO with transparency
magick badge.svg -transparent "#F0F0F0" -define icon:auto-resize=32,64,128 favicon.ico
```

#### Transparency Handling
```bash
# Remove white background
magick input.png -transparent white -define icon:auto-resize=16,32,64 favicon.ico

# SVG with specific resolution and transparency
magick input.svg -resize 512x512 -define icon:auto-resize=512,256,128 favicon.ico
```
