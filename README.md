# ARRI Frameline Visualizer

A web-based tool for visualizing ARRI Alexa Mini framelines and corner blackouts. Upload your camera's XML files to preview exactly how your framelines will appear in-camera. Perfect for cinematographers and DITs who need to verify framing guides before shooting.

The live demo is hosted here: `https://www.jenssage.com/arri-frameline-visualizer/`

## How to Use

### 1. Visualizer
- Open `framelines-visualizer.html` in any web browser
- **Load your XML**: Click "Choose File" under "Load Framelines XML File"
- **Load a background image** (optional): Click "Choose File" under "Load Background Image"
  - The visualizer will try to load an external image, but due to CORS restrictions this may not work
  - Upload your own image file (JPG, PNG) to see exactly how the framelines look over your footage
- The visualizer shows:
  - **Black areas**: Your corner blackouts (100% opacity)
  - **Gray areas**: Original shading (25% opacity)  
  - **Green lines**: Frame lines (16:9 and vertical format guides)
  - **Neutral grey background**: Shown when no image is loaded

### 2. Loading on Camera
- Copy the `A-Mini_4x3-2_8K_1_0_modified.xml` file to your camera's media
- Load it through the Alexa Mini's frame lines menu
- The corner blackouts will appear in your viewfinder and SDI outputs

### 3. Customizing Corner Size
To adjust the size of the corner blackouts, edit the XML file. Remember that the corners align with the **16:9 frame**, which spans from **0.125 to 0.875** vertically in the full 4:3 sensor.

**Current settings (15% width, extending to mid-frame):**
```xml
<!-- Top corners -->
<top>0.125</top>      <!-- Start at top of 16:9 frame -->
<bottom>0.75</bottom>  <!-- Extend to 75% down = middle of 16:9 frame -->
<left>0</left>         <!-- or <left>0.85</left> for right side -->
<right>0.85</right>    <!-- 15% from edge -->
```

**Smaller corners (10% width, less vertical extent):**
```xml
<top>0.125</top>
<bottom>0.70</bottom>  <!-- Less vertical coverage -->
<left>0</left>
<right>0.90</right>    <!-- 10% from edge -->
```

**Larger corners (20% width, more vertical extent):**
```xml
<top>0.125</top>
<bottom>0.80</bottom>  <!-- More vertical coverage -->
<left>0</left>
<right>0.80</right>    <!-- 20% from edge -->
```

**Important**: The `<top>` value should always be `0.125` (16:9 frame top edge) and the bottom corners' `<bottom>` value should always be `0.125` (16:9 frame bottom edge) to align with your 16:9 extraction.

## Technical Notes

According to ARRI's specification sheet, the Alexa Mini in 4:3 2.8K mode has:
- Sensor photosites: 2880 × 2160
- Physical sensor size: 23.76mm × 17.82mm
- Image circle: 29.70mm
- Aspect ratio: 1.33 (4:3)

The corner blackouts work because they use normalized coordinate values (0.0 to 1.0), which are resolution-independent. This means the same XML structure works regardless of the actual pixel dimensions.

## Support

If you need to adjust the corner sizes or have questions about the implementation, you can:
1. Use the visualizer to preview changes before loading on camera
2. Edit the XML directly (it's just a text file)
3. Refer to ARRI's Frame Line Tool for more details:
   - [ARRI Frame Line Tool](https://tools.arri.com/flt/index.html)

---

Created: October 24, 2025
Based on ARRI FLT-5.3.1 format specification
