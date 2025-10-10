# Implementation Plan

- [x] 1. Create basic HTML structure and Phaser.js setup


  - Create single HTML file with embedded CSS and JavaScript
  - Include Phaser.js via CDN
  - Set up basic game scene with canvas
  - Initialize game configuration and scene management
  - _Requirements: 7.1, 7.2, 7.3_



- [x] 2. Implement grid system and visual layout





  - Create grid-based coordinate system for circuit placement
  - Implement grid-to-world and world-to-grid position conversion functions
  - Draw visual grid lines on the playing field


  - Set up item bank area beside the playing field
  - _Requirements: 1.1, 2.1_

- [x] 3. Create circuit components and initial layout





  - Implement battery sprite with positive/negative terminals


  - Create light bulb sprite with on/off states
  - Add pre-placed wire segments to guide the solution
  - Define gap positions where items need to be placed
  - _Requirements: 1.2, 1.3, 1.4_



- [x] 4. Build item bank with conductor and insulator materials





  - Create draggable item sprites with labels (copper, rubber, metal, wood, etc.)
  - Implement item bank layout and organization
  - Add visual distinction between conductors and insulators using colors
  - Set up item quantities and availability
  - _Requirements: 2.2, 2.3, 2.4_



- [x] 5. Implement drag-and-drop functionality





  - Add mouse/touch input handling for item selection
  - Create drag preview with semi-transparent item following cursor
  - Implement drop zone validation for grid positions


  - Handle item placement and return-to-bank logic for invalid drops
  - Prevent overlapping with existing circuit components
  - _Requirements: 3.1, 3.2, 3.3, 3.4, 3.5_

- [x] 6. Create circuit evaluation system


  - Implement breadth-first search algorithm for path finding
  - Check for complete conductive path from battery positive to negative terminal
  - Ensure path includes the light bulb in the circuit
  - Handle conductor vs insulator logic in path evaluation
  - _Requirements: 4.1, 4.2, 4.3, 4.4, 4.5_




- [x] 7. Add test circuit functionality and visual feedback







  - Create "Test Circuit" button in the UI
  - Implement circuit testing when button is clicked
  - Update light bulb visual state (lit/unlit) based on circuit evaluation
  - Add visual current flow animation for successful circuits
  - _Requirements: 5.1, 5.2, 5.3, 5.4, 5.5_

- [x] 8. Implement success modal and game completion







  - Create success modal popup for correct solutions
  - Add congratulatory message and visual effects
  - Include "Play Again" or "New Level" options in modal
  - Handle game reset functionality
  - _Requirements: 6.1, 6.2, 6.3_

- [x] 9. Polish visual design and user experience



  - Apply color scheme for conductors (metallic) and insulators (non-metallic)
  - Add hover effects and visual feedback for interactive elements
  - Implement smooth animations for drag-and-drop interactions
  - Add particle effects or glow for successful circuit completion
  - Ensure responsive layout works on different screen sizes
  - _Requirements: 1.1, 2.4, 3.2, 5.5, 6.1_

- [x] 10. Implement item removal functionality





  - Add drag-based removal system for placed circuit items
  - Implement distance threshold detection for removal trigger
  - Create returnItemToBank function to restore items to item bank
  - Add visual feedback during removal process
  - Prevent removal of pre-placed components (battery, bulb, wires)
  - _Requirements: 7.1, 7.2, 7.3, 7.4, 7.5_

- [x] 11. Create visual connection system for continuous wiring








  - Implement dynamic wire rendering between adjacent conductive components
  - Create connection graphics that show continuous electrical paths
  - Add proper terminal connections from battery to circuit components
  - Ensure seamless wire connections bridge circuit gaps
  - Update connection visuals when items are placed or removed
  - _Requirements: 8.1, 8.2, 8.3, 8.4, 8.5_

- [x] 12. Fix reset button to clear entire game state





  - Modify reset function to remove all placed items from circuit
  - Restore all items to original quantities in item bank
  - Clear all gap positions back to empty state
  - Turn off light bulb and clear any success states
  - Redraw base circuit with only pre-placed components
  - _Requirements: 9.1, 9.2, 9.3, 9.4, 9.5_

- [x] 13. Expand grid size to 15x15 for more complex circuit designs
  - Update gameState configuration to use 15x15 grid dimensions
  - Modify canvas size to accommodate larger grid (900x900 pixels)
  - Reposition battery and bulb components to center of expanded grid
  - Update circuit layout with more gaps and wire segments for complex designs
  - Ensure responsive design works with larger grid on different screen sizes
  - _Requirements: 1.1, 1.5, 10.1, 10.2, 10.3, 10.4, 10.5_

- [x] 14. Fix missing part indicators by removing black overlay and size display
  - Remove black overlay (sizeIndicator) from gap marking function
  - Remove size text display from missing part indicators
  - Remove text labels completely from missing part indicators
  - Fix positioning of multi-cell gaps to prevent wire overlap
  - Fix gap positioning consistency during drag operations
  - Reposition 3x1 missing part indicator to bottom wire path and center it
  - Improve visual balance by spacing top gaps equally
  - Update wire layout to accommodate repositioned gaps
  - Ensure dashed outline remains clear and visible without visual clutter
  - _Requirements: 12.1, 12.2, 12.3, 12.4, 12.5, 12.6, 12.7, 12.8_

- [x] 15. Fix item positioning for multi-cell items (2x1, 3x1)
  - Correct positioning calculation in createGameSprite function for multi-cell items
  - Ensure 2x1 and 3x1 items are properly centered within their grid space
  - Fix overlap issues with pre-existing wires and circuit components
  - Update gridToWorld positioning to account for item size properly
  - Improve item label positioning and styling with proper background
  - Verify electrical connections work correctly for all contact points of multi-cell items
  - _Requirements: 13.1, 13.2, 13.3, 13.4, 13.5, 13.6_

- [x] 16. Fix item tooltips to show size information and resolve scroll positioning issues





  - Implement size information display in tooltip content using the format "Item Name (X cell)" or "Item Name (X cells)"
  - Update tooltip HTML to display item name and size in parentheses (e.g., "Coin (1 cell)", "Metal Rod (3 cells)", "Copper Wire (2 cells)")
  - Fix tooltip positioning calculation to use element-relative coordinates instead of viewport coordinates
  - Implement getBoundingClientRect() or similar method to get accurate item position including scroll offset
  - Center tooltip horizontally above the item using the item's actual screen position
  - Ensure tooltip positioning remains accurate when page is scrolled up or down
  - Change background color to light purple for better visibility
  - Test tooltip positioning at different scroll positions to verify it stays anchored to the item
  - Maintain clean, simple tooltip styling with readable formatting
  - Verify tooltip hide functionality works properly on mouse leave
  - _Requirements: 14.1, 14.2, 14.3, 14.4, 14.5, 14.6, 14.7, 14.8, 14.9, 14.10_

- [ ] 17. Implement multi-stage system and stage progression
  - Create stage management system to track current stage
  - Add stage configuration objects for different circuit layouts
  - Implement stage switching functionality to load different circuit configurations
  - Update success modal to include "Next Stage" button for stage progression
  - Create stage reset functionality that clears current stage without affecting progression
  - _Requirements: 15.1, 15.2, 17.1, 17.3, 17.4, 17.7_

- [ ] 18. Create Stage 2 circuit layout with parallel paths
  - Design Stage 2 circuit configuration with battery on left and bulb on right
  - Position three missing parts: rectangular at top center, square at middle left, rectangular at bottom left
  - Center the entire Stage 2 circuit layout within the 15x15 grid
  - Create wire framework showing top path and bottom path connections
  - Implement proper branching and rejoining wire connections for parallel circuit design
  - _Requirements: 15.3, 15.4, 15.5, 15.6, 16.1, 16.3, 16.4, 16.5, 16.6_

- [ ] 19. Update circuit evaluation system for parallel paths
  - Modify circuit evaluation to support multiple parallel paths in Stage 2
  - Ensure breadth-first search algorithm can find any valid conductive route
  - Update path finding to handle branching circuits with multiple valid solutions
  - Maintain same electrical principles (conductors allow flow, insulators block flow)
  - Test circuit completion when any parallel path provides complete connection
  - _Requirements: 15.7, 15.8, 17.2, 17.5_

- [ ] 20. Implement visual connection system for parallel circuits
  - Update wire rendering system to handle branching and rejoining connections
  - Create dynamic wire connections that show parallel paths clearly
  - Ensure continuous wire visualization works with multiple circuit branches
  - Update connection graphics to demonstrate current flow through parallel paths
  - Maintain visual clarity when showing multiple conductive routes simultaneously
  - _Requirements: 16.2, 16.7, 16.8_

- [ ]* 21. Add educational enhancements and additional features
  - Include explanatory text about conductors and insulators
  - Add sound effects for interactions and success
  - Create additional difficulty levels with different circuit layouts
  - Add hint system to guide players toward correct solutions
  - _Requirements: 4.1, 4.2, 4.3_ 