# D&D Paper Miniature Maker - Design Specification (Updated for 2-Sided Miniatures)

## Project Overview
Create a standalone web application for designing custom paper miniatures for Dungeons & Dragons and tabletop RPGs. The application will run entirely offline in a web browser, allowing users to create printable 2-sided miniature designs by combining shapes, images, and customizations on both front and back sides.

## Core Features

### 1. Dual-Sided Canvas Interface
- Fixed-size drawing canvas (800x600px) representing the printable area
- Visual division showing front and back sides clearly marked
- Front and back sections positioned side-by-side or stacked for easy printing
- Cut lines indicated around each miniature for easy cutting
- Registration marks/guides to help align front and back when gluing
- White background with subtle shadow for depth perception
- Touch and mouse support for interaction

### 2. Shape Tools
- **Circle Tool**: Create circular bases for miniatures (25mm/1 inch standard available)
- **Square Tool**: Create square/rectangular bases
- Color selection via HTML color picker
- Size adjustment via numeric input (in pixels with mm/pixel conversion)
- Placement via click/touch on canvas
- Option to snap to standard base sizes (25mm circle, 25mm square, etc.)

### 3. Image Handling
- Image upload button (accepts common image formats: PNG, JPG, GIF, SVG)
- Images appear on canvas and can be positioned/sized
- Support for transparent PNGs for best results
- Client-side image processing only (no uploads to external servers)
- Ability to place images on either front or back side independently

### 4. Object Manipulation
- **Select Tool** (arrow icon): Choose and manipulate existing objects
- **Drag to Move**: Selected objects can be dragged to new positions
- **Delete Functionality**: Selected objects can be removed via Delete key or visual cue
- **Selection Visualization**: Gold dashed outline with delete hints
- **Copy/Paste Functionality**: Duplicate selected objects (Ctrl+C/Ctrl+V or buttons)
- Ability to copy objects between front and back sides

### 5. Customization Options
- Color picker for shape fills
- Size input fields for precise dimension control (pixels and mm)
- Real-time preview of changes
- Default sizes suitable for standard miniature bases (25mm)
- Ability to set exact sizes for precise alignment between front/back

### 6. 2-Sided Specific Features
- **Front/Back Toggle**: Easily switch between editing front and back sides
- **Independent Editing**: Each side maintains its own object list
- **Alignment Guides**: Visual guides to help align corresponding elements between front and back
- **Base Alignment Tools**: Tools to ensure bases line up properly when glued
- **Preview Mode**: See how front and back will align when assembled
- **Cut Lines**: Dashed lines showing where to cut out each miniature
- **Assembly Indicators**: Visual cues showing which edges should be glued together

### 7. Export Capabilities
- **PNG Export**: High-quality raster image showing both front and back sides
- **PDF Export**: Vector-based PDF for scalable printing with cut lines
- **Filename Convention**: Default names with descriptive prefixes
- **Client-Side Generation**: No server upload required
- **Print Layout**: Optimized layout for standard paper sizes (Letter/A4)

### 8. User Experience Features
- **Dark Theme**: D&D-inspired color scheme (dark blues with gold accents)
- **Responsive Design**: Adapts to different screen sizes
- **Touch Support**: Full functionality on touch-enabled devices
- **Keyboard Shortcuts**: Delete key removes selected objects, Ctrl+C/V for copy/paste
- **Instructional Overlay**: Clear guidance for first-time users
- **Status Bar**: Real-time feedback on current actions and selected side

## Technical Architecture

### Frontend Technologies
- **HTML5**: Semantic structure with canvas element
- **CSS3**: Modern styling with CSS variables and flexbox
- **Vanilla JavaScript**: No external frameworks for simplicity
- **HTML5 Canvas API**: Core drawing and manipulation functionality
- **jsPDF Library**: External library for PDF generation (via CDN)

### Core Components
1. **MiniatureMaker Class**: Main application controller
2. **DualCanvas Manager**: Handles front/back canvas states and rendering
3. **Object Model**: Generic object structure for shapes and images with side identification
4. **Tool Manager**: Handles current tool state and interactions
5. **Export Manager**: Handles PNG and PDF generation with layout
6. **UI Controller**: Manages DOM elements and event listeners
7. **Alignment Guide System**: Visual guides for front/back alignment

### Data Model
Objects are stored in separate arrays for front and back sides with this structure:
```javascript
{
  id: string,              // Unique identifier
  type: 'circle' | 'square' | 'image',
  x: number,               // x-coordinate (relative to side)
  y: number,               // y-coordinate (relative to side)
  side: 'front' | 'back',  // Which side the object belongs to
  color: string,           // Hex color (for shapes)
  // Shape-specific properties:
  radius: number,          // for circles
  width: number,           // for squares/images
  height: number,          // for squares/images
  // Image-specific:
  src: string              // Data URL for uploaded images
}
```

### Interaction Flow
1. User selects side to edit (front/back toggle)
2. User selects tool (select/circle/square)
3. User sets properties (color, size)
4. For shape tools: Click on canvas creates object at click location on selected side
5. For select tool: Click selects object under cursor on current side
6. Selected objects can be dragged to new position on current side
7. Objects can be copied/pasted between sides
8. Objects can be deleted via keyboard or selection hint
9. Export functions generate files showing both sides with layout and cut lines

## Design Decisions & Trade-offs

### Why Dual-Sided Single Canvas Approach?
- **Print Optimization**: Single printable page with front/back clearly laid out
- **User Familiarity**: Builds on existing single-canvas workflow users know
- **Cutting Guidance**: Visual cut lines show exactly where to cut
- **Assembly Guidance**: Registration marks help align front/back when gluing
- **Trade-off**: Requires careful layout planning but provides clear printable output

### Standard Base Sizes
- **25mm Circle**: Standard D&D miniature base
- **25mm Square**: Alternative base shape
- **30mm Circle**: For larger creatures
- **1 inch equivalents** for imperial users
- Users can still create custom sizes as needed

### Alignment System
- Visual guides appear when objects are near corresponding positions on opposite sides
- Snap-to-grid options for precise alignment
- Base alignment tools ensure bottom edges match for proper gluing

## User Interface Design

### Color Scheme
- **Primary Background**: Deep blue gradient (#1e3c72 to #2a5298)
- **Secondary Background**: Semi-transparent black overlay (rgba(0,0,0,0.3))
- **Accent Color**: Metallic gold (#ffd700) for active elements and highlights
- **Text Color**: White for contrast on dark backgrounds
- **Canvas Background**: Pure white for accurate color representation
- **Side Differentiation**: Subtle tint differences between front/back areas
- **Cut Lines**: Dashed red lines showing cut boundaries
- **Alignment Guides**: Dashed golden lines showing corresponding positions

### Layout Structure
1. **Header**: Application title with thematic styling
2. **Toolbar**: Horizontal arrangement of tools and controls
3. **Side Selector**: Toggle between front/back editing views
4. **Canvas Area**: Central drawing surface showing both sides with clear division
5. **Status Bar**: Bottom feedback area
6. **Instructions**: Collapsible help section at bottom

### Visual Indicators
- **Active Side Indicator**: Clear highlight showing which side is being edited
- **Object Side Indicators**: Small icons showing which side objects belong to
- **Selection Indicators**: Different styles for front vs. back selected objects
- **Alignment Preview**: Ghosted preview showing where objects would align on opposite side

## Error Handling & Edge Cases

### Image Loading
- Invalid files show graceful error handling
- Large images automatically scaled to fit canvas boundaries
- Placeholder rendering while images load
- Warning if images extend beyond printable area

### Object Manipulation
- Boundary checking prevents objects from being dragged completely off-canvas
- Selection prioritizes topmost objects in overlapping scenarios
- Minimum size constraints prevent unusably small objects
- Warning when objects are too close to cut lines

### Export Limitations
- Very complex designs may affect export performance (mitigated by reasonable canvas size)
- Browser print dialog handles actual paper sizing and scaling
- Clear indication of printable area vs. non-printable margins

## Future Enhancement Possibilities

### Post-MVP Features
1. **Template Library**: Pre-made bases for common miniature types
2. **Text Tool**: Add character names or stats directly on miniature
3. **Layer Management**: Control object stacking order within each side
4. **Advanced Duplicate**: Options for mirrored duplication between sides
5. **Multiple Miniatures Per Page**: Layout optimization for sheets of multiple miniatures
6. **Different Base Styles**: Slotted bases, textured bases, etc.
7. **Preview Animation**: Show how miniature assembles from flat to 3D
8. **Material Suggestions**: Recommendations for paper types, adhesives, etc.

### Technical Improvements
1. **Service Worker**: True offline PWA capabilities
2. **Web Workers**: Offload image processing for better performance
3. **Advanced Export**: SVG generation alongside PNG/PDF
4. **Custom Paper Sizes**: User-definable dimensions for different paper formats
5. **Theme Support**: Alternative color schemes (printer-friendly, high contrast, etc.)
6. **Batch Export**: Generate multiple miniatures on a single sheet for efficiency

## Success Criteria

### Functional Requirements
- [ ] Users can create circular and square shapes on both front and back sides
- [ ] Users can upload and position custom images on either side
- [ ] Users can customize colors and sizes independently for each side
- [ ] Users can select, move, delete, and copy objects on each side
- [ ] Users can copy objects between front and back sides
- [ ] Users can export designs as PNG and PDF files showing both sides with cut lines
- [ ] Application works completely offline
- [ ] Finished prints can be cut out and assembled into 2-sided miniatures

### Usability Requirements
- [ ] First-time users can create a 2-sided miniature within 3 minutes
- [ ] Interface is intuitive for both single-sided and 2-sided workflows
- [ ] Visual feedback clearly indicates which side is being edited
- [ ] Alignment guides help users create properly aligned miniatures
- [ ] Application is responsive on desktop and tablet devices
- [ ] Touch interactions are smooth and precise for both sides

### Technical Requirements
- [ ] Application loads in <3 seconds on average connection
- [ ] No errors in browser console during normal operation
- [ ] Export files are correctly formatted, printable, and include cut lines
- [ ] Memory usage remains reasonable during extended use
- [ ] Works in modern browsers (Chrome, Firefox, Safari, Edge)
- [ ] Exported PDFs maintain vector quality for scalable printing

## Implementation Plan Reference
See the implementation plan created with the `writing-plans` skill for detailed development steps, task breakdown, and implementation order.