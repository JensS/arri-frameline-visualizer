# ARRI Frameline Visualizer

A web-based tool for visualizing ARRI camera framelines and corner blackouts across multiple ARRI camera models and formats. Upload your camera's XML files to preview exactly how your framelines will appear in-camera. Perfect for cinematographers and DITs who need to verify framing guides before shooting.

The live demo is hosted here: [https://www.jenssage.com/arri-frameline-visualizer/](https://www.jenssage.com/arri-frameline-visualizer/)

## Features

- **Multi-Camera Support**: Works with ALEXA 35, ALEXA 35 Xtreme, ALEXA 265, ALEXA LF, ALEXA Mini LF, AMIRA, and more
- **Format Selection**: Choose from all available sensor formats for your camera (Open Gate, 16:9, 4:3, 6:5, anamorphic, etc.)
- **Aspect Ratio Validation**: Automatically validates uploaded images against the selected format
- **Multiple Background Options**: Grey grid, sample images, or custom uploads
- **XML Library**: Pre-loaded example frameline configurations
- **Real-time Visualization**: See exactly how framelines will appear with proper aspect ratios

## How to Use

### 1. Select Your Camera and Format
- **Select Camera Model**: Choose your ARRI camera from the dropdown (e.g., ALEXA 35, ALEXA Mini LF)
- **Select Format**: Choose the recording format you'll be using (e.g., 4.6K 3:2 Open Gate, 4K 16:9, etc.)
- The visualizer automatically adjusts the canvas aspect ratio to match your selected format
- Camera format information is displayed in the info panel below

### 2. Load Framelines XML
- **Load your XML**: Click "Choose File" or "Select from Library"
- Select from pre-loaded examples or upload your own XML file
- The visualizer shows:
  - **Black areas**: Corner blackouts (100% opacity)
  - **Gray areas**: Shading overlays (25% opacity)
  - **Green lines**: Frame lines for different aspect ratios
  - **Neutral grey background**: Default when no image is loaded

### 3. Background Options
- **Upload Custom Image**: Load your own reference image (JPG, PNG)
  - The app validates that your image matches the selected format's aspect ratio
  - Warnings appear if there's a mismatch (5% tolerance)
- **Use Sample Image**: Load the included sample image (4:3 format)
- **Use Grey Grid**: Display a reference grid for framing

### 4. Loading on Camera
- Copy your XML file to a USB stick with a folder structure created with the camera itself
- Load it through your ARRI camera's frame lines directory
- The framelines will appear in your viewfinder and SDI outputs based on your preferences

## Technical Notes

### Camera Format Database

The visualizer includes comprehensive format data for the following cameras:
- **ALEXA 35 Xtreme** (Premium & Base variants)
- **ALEXA 35** (Premium & Base variants)
- **ALEXA 35 HVNF**
- **ALEXA 265**
- **ALEXA Mini LF**
- **AMIRA & ALEXA Mini**
- **ALEXA 65**
- **ALEXA XT**
- **ALEXA**
- **ALEXA SXT**
- **ALEXA LF**

Each format includes:
- Sensor photosites (resolution)
- Physical sensor dimensions in mm and inches
- Image circle diameter
- Recording resolution options
- Supported codecs (ARRIRAW, ProRes, ARRICORE)

### Aspect Ratio Validation

The app validates uploaded images with a 5% tolerance. For example:
- **4:3 format** (1.33:1): Accepts images between 1.26:1 and 1.40:1
- **16:9 format** (1.78:1): Accepts images between 1.69:1 and 1.87:1
- **2.39:1 format**: Accepts images between 2.27:1 and 2.51:1

### Normalized Coordinates

Framelines use normalized coordinate values (0.0 to 1.0), which are resolution-independent. This means the same XML structure works across different recording resolutions and formats, as long as the aspect ratio matches.

## Support

If you need to adjust the corner sizes or have questions about the implementation, you can:
1. Use the visualizer to preview changes before loading on camera
2. Edit the XML directly (it's just a text file)
3. Refer to ARRI's Frame Line Tool for more details:
   - [ARRI Frame Line Tool](https://tools.arri.com/flt/index.html)

---

Created: October 24, 2025
Based on ARRI FLT-5.3.1 format specification
