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

- [x] 17. Replace game items with image assets









  - Update battery sprite to use battery.png image asset
  - Update light bulb sprite to use light-bulb.png spritesheet (left half for off state, right half for on state)
  - Replace item bank items with corresponding image assets (coin.png, bottlecap.png, key.png, etc.)
  - Update item definitions to use proper image dimensions and positioning
  - Ensure image loading and display works correctly in Phaser.js
  - Maintain existing drag-and-drop functionality with image sprites
  - _Requirements: 2.4, 4.1_

- [x] 18. Implement multi-stage system and stage progression





  - Create stage management system to track current stage
  - Add stage configuration objects for different circuit layouts
  - Implement stage switching functionality to load different circuit configurations
  - Update success modal to include "Next Stage" button for stage progression
  - Create stage reset functionality that clears current stage without affecting progression
  - _Requirements: 15.1, 15.2, 17.1, 17.3, 17.4, 17.7_

- [ ] 19. Create Stage 2 circuit layout with parallel paths
  - Design Stage 2 circuit configuration with battery on left and bulb on right
  - Position three missing parts: rectangular at top center, square at middle left, rectangular at bottom left
  - Center the entire Stage 2 circuit layout within the 15x15 grid
  - Create wire framework showing top path and bottom path connections
  - Implement proper branching and rejoining wire connections for parallel circuit design
  - _Requirements: 15.3, 15.4, 15.5, 15.6, 16.1, 16.3, 16.4, 16.5, 16.6_

- [ ] 20. Update circuit evaluation system for parallel paths
  - Modify circuit evaluation to support multiple parallel paths in Stage 2
  - Ensure breadth-first search algorithm can find any valid conductive route
  - Update path finding to handle branching circuits with multiple valid solutions
  - Maintain same electrical principles (conductors allow flow, insulators block flow)
  - Test circuit completion when any parallel path provides complete connection
  - _Requirements: 15.7, 15.8, 17.2, 17.5_

- [ ] 21. Implement visual connection system for parallel circuits
  - Update wire rendering system to handle branching and rejoining connections
  - Create dynamic wire connections that show parallel paths clearly
  - Ensure continuous wire visualization works with multiple circuit branches
  - Update connection graphics to demonstrate current flow through parallel paths
  - Maintain visual clarity when showing multiple conductive routes simultaneously
  - _Requirements: 16.2, 16.7, 16.8_

- [x] 22. Fix drag preview scaling to maintain original item size



  - Remove the scale(0.9) transformation from the drag preview creation
  - Ensure drag preview uses full size (1.0 scale) to match original item dimensions
  - Update createDragPreview function to maintain consistent item sizing during drag operations
  - Verify that multi-cell items maintain proper proportions during drag
  - _Requirements: 18.1, 18.2, 18.3, 18.4, 18.5_

- [x] 25. Clear red line indicators when switching stages





  - Update stage switching functionality to clear any existing red current flow animations
  - Ensure red line indicators from short circuit conditions are removed when loading new stages
  - Clear any visual artifacts from previous short circuit states during stage transitions
  - _Requirements: 19.11_

- [x] 32. Fix Stage 4 circuit evaluation and current flow issues
  - Fixed findFourthCircuitPath function to properly evaluate parallel circuit paths independently
  - Updated left bulb to light when only 2-cell gap is filled with conductors, regardless of other gaps
  - Fixed success modal to only appear when ALL bulbs are lit, not just one
  - Fixed buildRightBulbPath to only build path when right bulb is actually lit and all required gaps are filled
  - Fixed buildLeftBulbPath to only build path when left bulb is lit and 2-cell gap is filled
  - Fixed drawFourthCircuitPath to only draw yellow line paths for lit bulbs (removed unconditional line to (7,4))
  - Updated circuit evaluation to handle Stage 4 dual bulbs correctly without overriding bulb states
  - Added comprehensive debugging to path building and particle creation functions
  - Added debugging to gap detection and item placement verification
  - **FIXED: Charge particles now display across left bulb's current path when only left bulb is switched on**
  - Fixed missing `active` property on particles that was preventing animation from starting
  - Fixed test circuit logic to show flow visualization for Stage 4 partial completion (when only one bulb is lit)
  - Added special handling in test circuit button to call `visualizeCurrentFlow(true)` when any bulb is lit in Stage 4
  - Charges now flow through the complete left circuit path: battery positive → (2,4) → gaps (3,4)-(4,4) → (5,4) → (6,4) → (6,5) → left bulb → (6,9) → (6,10) → (5,10) → (4,10) → (3,10) → (2,10) → (1,10) → battery negative
  - Verified charge particle animation works correctly for partial circuit completion in Stage 4
  - _Requirements: 24.1, 24.2, 24.3, 24.4, 24.5, 24.6, 24.7, 24.8_

- [ ]* 23. Add educational enhancements and additional features
  - Include explanatory text about conductors and insulators
  - Add sound effects for interactions and success
  - Create additional difficulty levels with different circuit layouts
  - Add hint system to guide players toward correct solutions
  - _Requirements: 4.1, 4.2, 4.3_ 
- [x] 24. Implement short circuit detection and warning system for Stage 2



  - Create detectShortCircuit function to identify when conductor is placed in critical 3-slot position (6,6) to (6,8)
  - Implement findDirectBatteryPath function to detect paths that bypass the light bulb
  - Update circuit evaluation system to check for short circuits before normal evaluation
  - Create red current flow animation for short circuit conditions instead of normal yellow flow
  - Keep light bulb off when short circuit is detected
  - Create short circuit warning modal with age-appropriate explanation of short circuits and safety hazards
  - Include educational content about what short circuits are and how to avoid them
  - Add "Try Again" and "Reset Circuit" options to the warning modal
  - Ensure short circuit detection only applies to Stage 2 circuit layout
  - _Requirements: 19.1, 19.2, 19.3, 19.4, 19.5, 19.6, 19.7, 19.8, 19.9, 19.10_

- [x] 26. Add educational "What you learned" section to Stage 2 success modal





  - Modify Stage 2 success modal to include a "What you learned" section below the congratulatory content
  - Add age-appropriate explanation of what short circuits are and why they're dangerous
  - Explain that short circuits happen when electricity takes an unintended shortcut path
  - Include information about how short circuits can be dangerous due to excessive current flow
  - Mention real-world safety concerns like equipment damage and fire hazards
  - Explain how parallel circuits (like Stage 2) provide multiple safe paths for electricity
  - Use simple, child-friendly language appropriate for the target audience
  - Maintain celebratory tone while adding educational value
  - Ensure the educational content enhances rather than overwhelms the success experience
  - _Requirements: 20.1, 20.2, 20.3, 20.4, 20.5, 20.6, 20.7, 20.8, 20.9, 20.10_

- [ ] 27. Create Stage 3 "Series Circuit" layout with dual light bulbs
  - Design Stage 3 circuit configuration with battery positioned at (1, 4) to (1, 8)
  - Position two light bulbs at (7, 3) to (9, 3) and (7, 11) to (9, 11)
  - Add L-shaped wires at positions (1, 4), (1, 10), (10, 4), and (10, 10)
  - Create straight wire connections forming a complete series circuit path
  - Position missing part indicators at (4, 4) to (6, 4), (4, 10) to (6, 10), (6, 6) to (6, 8), and (12, 6) to (12, 8)
  - Center the entire Stage 3 circuit layout within the 15x15 grid
  - _Requirements: 21.4, 21.5, 21.6, 21.7, 21.8, 22.1, 22.2_

- [ ] 28. Implement series circuit evaluation logic for Stage 3
  - Update circuit evaluation system to handle dual light bulb configuration
  - Ensure both light bulbs light up simultaneously when circuit is complete
  - Implement logic that keeps both bulbs off if any gap exists or insulator is placed
  - Create path finding that verifies complete series connection through both bulbs
  - Update visual feedback to show current flow through the entire series path
  - _Requirements: 21.9, 21.10, 22.3, 22.4, 22.6, 22.7, 22.8_

- [x] 29. Add Stage 3 progression and educational content





  - Update Stage 2 success modal to include "Next Stage" button
  - Implement stage switching functionality to load Stage 3 from Stage 2
  - Add "Stage 3: Series Circuit" title display
  - Create Stage 3 success modal with educational "What you learned" section
  - Include age-appropriate explanation of series circuits and how they work
  - Explain that series circuits require all components to be connected in a single path
  - Add real-world examples like old Christmas lights or flashlights
  - Compare series circuits to parallel circuits from Stage 2
  - Clearly define what a series circuit is using simple terms like "components connected one after another in a chain"
  - Emphasize that all parts must work together for the circuit to function
  - Include visual metaphors that children can understand, such as comparing it to a chain where if one link breaks, the whole chain fails
  - _Requirements: 21.1, 21.2, 21.3, 23.1, 23.2, 23.3, 23.4, 23.5, 23.6, 23.7, 23.8, 23.9, 23.10, 23.11, 23.12, 23.13_

- [ ] 30. Update visual connection system for series circuit with dual bulbs
  - Modify wire rendering system to handle series circuit with two light bulbs
  - Create continuous wire connections showing battery → first bulb → second bulb → battery path
  - Update connection graphics to demonstrate series current flow through both bulbs
  - Ensure visual clarity when showing the single series path through multiple components
  - Maintain proper terminal connections for dual bulb configuration
  - _Requirements: 22.2, 22.5, 22.8_

- [ ] 31. Fix Stage 4 charge flow to follow proper wire paths instead of criss-crossing




  - Fix buildFourthCircuitPath function to create separate continuous paths for each bulb
  - Create left bulb path: battery positive → (1,4) → (2,4) → gaps (3,4)-(4,4) → (5,4) → (6,4) → (6,5) → left bulb → (6,9) → (6,10) → (5,10) → (4,10) → (3,10) → (2,10) → (1,10) → (1,9) → battery negative
  - Create right bulb path: battery positive → (1,4) → (2,4) → gaps (3,4)-(4,4) → (5,4) → (6,4) → (7,4) → gaps (8,4)-(10,4) → (11,4) → (12,4) → (12,5) → right bulb → (12,9) → (12,10) → (11,10) → (10,10) → gap (9,10) → (8,10) → (7,10) → (6,10) → (5,10) → (4,10) → (3,10) → (2,10) → (1,10) → (1,9) → battery negative
  - Ensure charges flow through continuous wire connections without jumping between disconnected positions
  - Remove the criss-crossing behavior where charges from (6,10) jump to (1,5) and charges from (1,9) jump to (6,4)
  - Test charge flow animation to verify proper electrical path visualization for both parallel circuits
  - _Requirements: Stage 4 charge flow accuracy and visual clarity_

- [ ] 33. Fix Stage 4 reset functionality to clear yellow line indicators
  - Update reset stage functionality to properly clear yellow line indicators for the left light bulb
  - Ensure all current flow visualizations (yellow lines and charge particles) are cleared when reset is triggered
  - Clear any active charge particle animations that may be running for the left bulb circuit
  - Reset all visual indicators to their default state when stage reset occurs
  - Verify that both left and right bulb visual states are properly reset to off position
  - Test reset functionality to ensure clean slate for Stage 4 after reset button is clicked
  - _Requirements: 9.4, 17.7_

- [x] 34. Create Stage 5: Series-Parallel Circuit
  - Copy Stage 4 configuration as the base for Stage 5
  - Change 3-cell missing slot at (8,4)-(10,4) to light bulb (bulb2)
  - Change right light bulb at (11,6)-(13,8) to 3-cell missing slot at (11,6)-(13,6)
  - Change 1-cell missing slot at (9,10) to light bulb (part of bottom wire)
  - Add new 1-cell missing slot at (3,10)
  - Update stage selector to include Stage 5 with "Series-Parallel Circuit" description
  - Implement findFifthCircuitPath function for series-parallel circuit evaluation
  - Create drawFifthCircuitPath function for visual path rendering
  - Add buildFifthCircuitPath function for charge particle animation
  - Update Stage 4 success modal to include "Next Stage" button to progress to Stage 5
  - Add Stage 5 completion modal with "Game Complete!" message
  - Ensure all circuit evaluation, visual rendering, and particle systems work correctly for Stage 5
  - _Requirements: Multi-stage progression, Series-parallel circuit design, Educational content_
- [x] 
36. Update Stage 5: Series-Parallel Circuit with 3 Bulbs and Vertical Gap
  - Change 3-cell missing slot from horizontal (11,6)-(13,6) to vertical orientation (9,5)-(9,7)
  - Move first light bulb from (5,6) to (6,6) - shift by 1 cell right
  - Add third light bulb at (8,9) to (10,11)
  - Update T-junction positions to (9,4), (7,10), and (9,10)
  - Update vertical wire positions to include (7,5), (7,9), (9,8)
  - Rewrite findFifthCircuitPath function to handle series-parallel circuit logic:
    - Left bulb (bulb1) needs 2-cell gap (3,4)-(4,4) AND 1-cell gap (3,10) filled (series connection)
    - Right bulbs (bulb2 and bulb3) need vertical 3-cell gap (9,5)-(9,7) filled (parallel connection)
  - Update drawFifthCircuitPath function for new circuit topology with 3 bulbs
  - Create buildFifthLeftBulbPath, buildFifthRightBulbPath, buildFifthThirdBulbPath functions
  - Update preplacedWires configuration for new bulb and gap positions
  - Add comprehensive educational "What You Learned" section about series-parallel circuits
  - Include explanations of how series and parallel connections work together
  - Add real-world examples of series-parallel circuits (house wiring, car electrical systems)
  - Ensure all circuit evaluation, visual rendering, and particle systems work correctly
  - _Requirements: Series-parallel circuit design, Educational content, Multiple bulb management_