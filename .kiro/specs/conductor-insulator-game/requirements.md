# Requirements Document

## Introduction

This feature involves creating an educational game for children to learn about electrical conductors and insulators through interactive circuit building. The game uses a grid-based playing field where players drag and drop materials to complete electrical circuits, with immediate feedback on whether their solutions work correctly based on real electrical principles.

## Requirements

### Requirement 1

**User Story:** As a child learning about electricity, I want to see a 15x15 grid-based playing field with a partially completed circuit, so that I can understand the basic structure of electrical circuits and have space for more complex designs.

#### Acceptance Criteria

1. WHEN the game loads THEN the system SHALL display a 15x15 grid-based playing field
2. WHEN the playing field is displayed THEN the system SHALL show a light bulb, battery, and pre-placed wires
3. WHEN the circuit is displayed THEN the system SHALL show missing gaps of varying sizes that need to be filled
4. WHEN the circuit is displayed THEN the system SHALL ensure the pre-placed wires guide toward a logical solution
5. WHEN the expanded grid is displayed THEN the system SHALL accommodate more complex circuit designs with additional space for creative solutions

### Requirement 2

**User Story:** As a child learning about materials, I want to see an item bank with different conductor and insulator materials, so that I can choose appropriate materials to complete the circuit.

#### Acceptance Criteria

1. WHEN the game loads THEN the system SHALL display an item bank beside the playing field
2. WHEN the item bank is displayed THEN the system SHALL show items ordered by ascending cell size: 1-cell items (Copper Coin, Bottle Cap, Lego Brick, Pebble, Button), 2-cell items (Metal Key, Paper Clip, Eraser, Rubber Band), and 3-cell items (Spoon, Metal Ruler, Popsicle Stick, Straw)
3. WHEN items are displayed THEN the system SHALL clearly label each item as either conductor or insulator
4. WHEN items are displayed THEN the system SHALL use colored blocks with text labels for visual representation

### Requirement 3

**User Story:** As a child interacting with the game, I want to drag items from the item bank to the playing field, so that I can build the electrical circuit by filling the gaps.

#### Acceptance Criteria

1. WHEN I click on an item in the item bank THEN the system SHALL allow me to drag it
2. WHEN I drag an item over the playing field THEN the system SHALL show visual feedback for valid drop zones
3. WHEN I drop an item on a valid gap THEN the system SHALL place the item in that position
4. WHEN I drop an item on an invalid location THEN the system SHALL return the item to the item bank
5. WHEN an item is placed THEN the system SHALL prevent overlapping with existing circuit components

### Requirement 4

**User Story:** As a child learning about electricity, I want the game to follow real electrical principles, so that I learn accurate information about how circuits work.

#### Acceptance Criteria

1. WHEN the circuit is evaluated THEN the system SHALL ensure current flows from positive to negative battery terminal
2. WHEN checking circuit completion THEN the system SHALL require a complete loop between battery and light bulb
3. WHEN conductors are placed in the circuit path THEN the system SHALL allow current to flow through them
4. WHEN insulators are placed in the circuit path THEN the system SHALL block current flow
5. WHEN the circuit has any gaps or insulators in the path THEN the system SHALL prevent the light bulb from lighting

### Requirement 5

**User Story:** As a child testing my circuit solution, I want to click a play button to test if my circuit works, so that I can get immediate feedback on my solution.

#### Acceptance Criteria

1. WHEN I have placed items in the circuit THEN the system SHALL display a play button
2. WHEN I click the play button THEN the system SHALL evaluate the complete circuit path
3. WHEN the circuit is complete with only conductors in the path THEN the system SHALL light up the bulb
4. WHEN the circuit is incomplete or contains insulators in the path THEN the system SHALL keep the bulb unlit
5. WHEN the evaluation is complete THEN the system SHALL provide visual feedback showing the result

### Requirement 6

**User Story:** As a child who successfully completes the circuit, I want to see a success message, so that I know I solved the puzzle correctly and feel accomplished.

#### Acceptance Criteria

1. WHEN the light bulb lights up after testing THEN the system SHALL display a success modal
2. WHEN the success modal appears THEN the system SHALL congratulate the player on their correct solution
3. WHEN the success modal is displayed THEN the system SHALL provide an option to play again or try a new level

### Requirement 7

**User Story:** As a child interacting with placed circuit components, I want to be able to remove items from the circuit once they are placed, so that I can correct mistakes and try different solutions.

#### Acceptance Criteria

1. WHEN I drag a placed item away from its circuit position THEN the system SHALL allow me to remove it
2. WHEN an item is dragged away from the circuit THEN the system SHALL return it to the item bank
3. WHEN an item is removed THEN the system SHALL clear that grid position for new placement
4. WHEN I try to drag pre-placed components (battery, bulb, wires) THEN the system SHALL NOT allow removal
5. WHEN an item is being dragged for removal THEN the system SHALL provide visual feedback showing the removal action

### Requirement 8

**User Story:** As a child building circuits, I want all components to be properly connected with continuous wiring, so that I can clearly see how electricity flows through a complete path.

#### Acceptance Criteria

1. WHEN battery terminals connect to circuit components THEN the system SHALL show continuous wire connections from battery terminals
2. WHEN circuit components are placed in gaps THEN the system SHALL show seamless wire connections bridging the gaps
3. WHEN components connect to the light bulb THEN the system SHALL show continuous wire path to bulb terminals
4. WHEN the complete circuit path is formed THEN the system SHALL display unbroken wire connections throughout the entire electrical path
5. WHEN electricity flows through the circuit THEN the system SHALL make the continuous conductive path visually apparent to demonstrate proper electrical flow

### Requirement 9

**User Story:** As a child who wants to start over, I want the reset button to clear both the item bank and the circuit I've built, so that I can begin fresh with a clean playing field.

#### Acceptance Criteria

1. WHEN I click the reset button THEN the system SHALL remove all placed items from the circuit
2. WHEN the reset button is clicked THEN the system SHALL return all items to their original quantities in the item bank
3. WHEN the game is reset THEN the system SHALL clear all gap positions back to empty state
4. WHEN the game is reset THEN the system SHALL turn off the light bulb if it was lit
5. WHEN the reset is complete THEN the system SHALL restore the original circuit layout with only pre-placed components

### Requirement 10

**User Story:** As a child who wants to build more complex circuits, I want the expanded 15x15 grid to support larger and more intricate circuit designs, so that I can explore advanced electrical concepts.

#### Acceptance Criteria

1. WHEN the grid is expanded to 15x15 THEN the system SHALL maintain the same cell size and visual clarity
2. WHEN more complex circuits are designed THEN the system SHALL support multiple parallel paths and branching circuits
3. WHEN the larger grid is used THEN the system SHALL allow for creative circuit layouts beyond simple linear connections
4. WHEN the expanded grid is displayed THEN the system SHALL maintain responsive design and fit appropriately on different screen sizes
5. WHEN complex circuits are built THEN the system SHALL continue to accurately evaluate electrical flow through all possible paths

### Requirement 11

**User Story:** As a user accessing this educational game, I want it to run in a web browser using a single HTML file, so that it's easy to access and share.

#### Acceptance Criteria

1. WHEN the game is developed THEN the system SHALL be built using Phaser.js framework
2. WHEN the game is packaged THEN the system SHALL be contained in a single HTML file
3. WHEN the HTML file is opened in a browser THEN the system SHALL load and run the complete game
4. WHEN the game runs THEN the system SHALL not require external image files for basic functionality

### Requirement 12

**User Story:** As a child learning about circuits, I want the missing part indicators to be clear and simple, so that I can easily see where items need to be placed without visual distractions.

#### Acceptance Criteria

1. WHEN missing parts are displayed THEN the system SHALL show only a dashed outline without any overlay
2. WHEN missing parts are displayed THEN the system SHALL NOT show size information, black backgrounds, or text labels
3. WHEN missing parts are displayed THEN the system SHALL use simple visual indicators that don't obstruct the circuit view
4. WHEN missing parts are displayed THEN the system SHALL maintain clear visibility of the underlying grid and circuit components
5. WHEN multi-cell missing parts are displayed THEN the system SHALL position them correctly to span their intended grid cells without overlapping wires
6. WHEN drag operations occur THEN the system SHALL maintain consistent positioning of missing part indicators without shifting or misalignment
7. WHEN the circuit layout is designed THEN the system SHALL position missing parts strategically across both top and bottom wire paths for varied gameplay
8. WHEN missing parts are positioned THEN the system SHALL ensure visual balance with equal spacing on top wire and centered positioning on bottom wire

### Requirement 13

**User Story:** As a child placing items in the circuit, I want multi-cell items to be positioned correctly within their designated spaces, so that they don't overlap with existing wires or components.

#### Acceptance Criteria

1. WHEN 2x1 or 3x1 items are placed THEN the system SHALL position them properly within their grid cells
2. WHEN multi-cell items are placed THEN the system SHALL ensure they do not overlap with pre-existing wires
3. WHEN items are positioned THEN the system SHALL center them appropriately within their allocated grid space
4. WHEN items are placed THEN the system SHALL maintain proper visual alignment with the circuit layout
5. WHEN multi-cell items are placed THEN the system SHALL ensure proper electrical connections at all contact points
6. WHEN items have labels THEN the system SHALL position labels above the items with proper styling and background

### Requirement 14

**User Story:** As a child exploring the item bank, I want item tooltips to show the item name and size information with accurate positioning, so that I can quickly identify items and understand their dimensions regardless of page scroll position.

#### Acceptance Criteria

1. WHEN I hover over an item in the item bank THEN the system SHALL display the item name and size in the tooltip using the format "Item Name (X cell)" or "Item Name (X cells)"
2. WHEN tooltips are displayed for multi-cell items THEN the system SHALL show the format "Item Name (X cells)" (e.g., "Metal Rod (3 cells)" for 3x1 items, "Copper Wire (2 cells)" for 2x1 items)
3. WHEN tooltips are displayed for single-cell items THEN the system SHALL show the format "Item Name (1 cell)" (e.g., "Coin (1 cell)")
4. WHEN tooltips appear THEN the system SHALL use clean, simple formatting with proper height and readable background
5. WHEN tooltips are shown THEN the system SHALL position them directly above the item being hovered on using relative positioning to the item element
6. WHEN the page is scrolled THEN the system SHALL maintain correct tooltip positioning relative to the hovered item without shifting
7. WHEN I move away from an item THEN the system SHALL hide the tooltip immediately
8. WHEN tooltips are displayed THEN the system SHALL use a light purple background color for better visibility
9. WHEN tooltips are positioned THEN the system SHALL be centered horizontally above the item and use element-relative coordinates instead of viewport coordinates
10. WHEN calculating tooltip position THEN the system SHALL account for the item's actual position on screen including any scroll offset

### Requirement 15

**User Story:** As a child who successfully completes the first circuit, I want to progress to a more challenging stage with multiple circuit paths, so that I can learn about parallel circuits and more complex electrical concepts.

#### Acceptance Criteria

1. WHEN I complete the first stage successfully THEN the system SHALL display a "Next Stage" button in the success modal
2. WHEN I click the "Next Stage" button THEN the system SHALL load Stage 2 with a more complex circuit layout
3. WHEN Stage 2 loads THEN the system SHALL display a circuit with multiple paths and branching connections
4. WHEN Stage 2 is displayed THEN the system SHALL show the battery positioned on the left side of the grid
5. WHEN Stage 2 is displayed THEN the system SHALL show the light bulb positioned on the right side of the grid
6. WHEN Stage 2 is displayed THEN the system SHALL show three missing parts: one rectangular part at top center, one square part at middle left, and one rectangular part at bottom left
7. WHEN Stage 2 circuit is evaluated THEN the system SHALL support multiple parallel paths for electrical flow
8. WHEN Stage 2 has a complete conductive path through any valid route THEN the system SHALL light up the bulb

### Requirement 16

**User Story:** As a child learning about parallel circuits, I want the Stage 2 circuit to be centered in the 15x15 grid with proper wire connections, so that I can clearly see how electricity can flow through multiple paths.

#### Acceptance Criteria

1. WHEN Stage 2 loads THEN the system SHALL center the entire circuit layout within the 15x15 grid
2. WHEN Stage 2 is displayed THEN the system SHALL show continuous wire connections forming the circuit framework
3. WHEN Stage 2 wires are displayed THEN the system SHALL create a top path connecting battery to bulb through the top missing part
4. WHEN Stage 2 wires are displayed THEN the system SHALL create a bottom path connecting battery to bulb through the bottom missing parts
5. WHEN Stage 2 wires are displayed THEN the system SHALL show proper branching where the circuit splits into multiple paths
6. WHEN Stage 2 wires are displayed THEN the system SHALL show proper rejoining where the multiple paths converge back together
7. WHEN items are placed in Stage 2 THEN the system SHALL maintain continuous wire connections between all conductive components
8. WHEN Stage 2 circuit is complete THEN the system SHALL visually demonstrate how current can flow through parallel paths

### Requirement 17

**User Story:** As a child working with the multi-stage game, I want the system to track my progress and maintain the same electrical principles across all stages, so that I have a consistent learning experience.

#### Acceptance Criteria

1. WHEN I switch between stages THEN the system SHALL maintain the same drag-and-drop functionality
2. WHEN I switch between stages THEN the system SHALL maintain the same conductor and insulator behavior
3. WHEN I switch between stages THEN the system SHALL reset the item bank to full quantities for each new stage
4. WHEN I switch between stages THEN the system SHALL clear any previously placed items
5. WHEN I am in Stage 2 THEN the system SHALL evaluate circuits using the same electrical flow principles as Stage 1
6. WHEN I complete Stage 2 THEN the system SHALL display the same success modal format as Stage 1
7. WHEN I use the reset button in any stage THEN the system SHALL reset only the current stage without affecting stage progression

### Requirement 18

**User Story:** As a child dragging items from the item bank, I want the items to maintain their original size during drag operations, so that I can clearly see what I'm placing without visual distraction.

#### Acceptance Criteria

1. WHEN I start dragging an item from the item bank THEN the system SHALL maintain the item's original size in the drag preview
2. WHEN the drag preview is displayed THEN the system SHALL NOT apply any scaling transformations that reduce the item size
3. WHEN dragging items THEN the system SHALL ensure the drag preview accurately represents the size of the item being placed
4. WHEN the drag preview is created THEN the system SHALL use the same visual dimensions as the original item in the bank
5. WHEN dragging multi-cell items THEN the system SHALL maintain proper proportions without size reduction
### R
equirement 19

**User Story:** As a child learning about electrical safety, I want to see what happens when I create a short circuit in Stage 2, so that I can understand the dangers of short circuits and learn how to avoid them.

#### Acceptance Criteria

1. WHEN I place conductors in BOTH the 2-slot missing part indicator at (3, 4) to (4, 4) AND the 3-slot missing part indicator from (6, 6) to (6, 8) in Stage 2 THEN the system SHALL create a short circuit condition
2. WHEN a short circuit is created THEN the system SHALL keep the light bulb off instead of lighting it up
3. WHEN a short circuit occurs THEN the system SHALL show electrical current and charges flowing from battery's + terminal through the 2-slot conductor at (3, 4) to (4, 4), through the (6, 4) T-shaped wire, through the 3-slot conductor at (6, 6) to (6, 8), through the (6, 10) T-shaped wire, then back to the battery's - terminal
4. WHEN a short circuit is active THEN the system SHALL display electrical charges and current flow indicators in red color instead of the usual yellow to indicate danger
5. WHEN I test a circuit with a short circuit condition THEN the system SHALL display a warning modal instead of a success modal
6. WHEN the short circuit warning modal appears THEN the system SHALL explain that a short circuit has been detected and the circuit needs to be updated
7. WHEN the short circuit warning modal is displayed THEN the system SHALL provide a brief, age-appropriate explanation about what a short circuit is and the possible hazards it may cause
8. WHEN the short circuit warning modal is displayed THEN the system SHALL include small tips on how to avoid short circuits in electrical systems
9. WHEN the short circuit explanation is provided THEN the system SHALL use language and content appropriate for audiences of all ages
10. WHEN the short circuit warning modal is shown THEN the system SHALL provide options to try again or reset the circuit
11. WHEN switching between stages THEN the system SHALL clear any existing red line indicators from previous short circuit conditions
#
## Requirement 20

**User Story:** As a child who successfully completes Stage 2, I want to see educational information about short circuits in the success modal, so that I can learn about electrical safety concepts even when I solve the circuit correctly.

#### Acceptance Criteria

1. WHEN I complete Stage 2 successfully without creating a short circuit THEN the system SHALL display the success modal with standard congratulatory content
2. WHEN the Stage 2 success modal is displayed THEN the system SHALL include a "What you learned" section
3. WHEN the "What you learned" section is shown THEN the system SHALL provide age-appropriate information about what short circuits are
4. WHEN the short circuit education is displayed THEN the system SHALL explain that short circuits happen when electricity takes an unintended shortcut path
5. WHEN the short circuit education is displayed THEN the system SHALL explain that short circuits can be dangerous because they allow too much electricity to flow too quickly
6. WHEN the short circuit education is displayed THEN the system SHALL mention that in real life, short circuits can damage equipment or cause fires
7. WHEN the short circuit education is displayed THEN the system SHALL explain how parallel circuits (like in Stage 2) can help prevent short circuits by providing multiple safe paths for electricity
8. WHEN the educational content is shown THEN the system SHALL use simple, child-friendly language appropriate for the target audience
9. WHEN the Stage 2 success modal is displayed THEN the system SHALL maintain the same congratulatory tone while adding the educational component
10. WHEN the "What you learned" section is included THEN the system SHALL not overwhelm the success celebration but enhance the learning experience

### Requirement 21

**User Story:** As a child who successfully completes Stage 2, I want to progress to Stage 3 "Series Circuit" with a more complex series circuit layout, so that I can learn about series circuits and how all components must be connected for the circuit to work.

#### Acceptance Criteria

1. WHEN I complete Stage 2 successfully THEN the system SHALL display a "Next Stage" button in the success modal
2. WHEN I click the "Next Stage" button from Stage 2 THEN the system SHALL load Stage 3 "Series Circuit"
3. WHEN Stage 3 loads THEN the system SHALL display the title "Stage 3: Series Circuit"
4. WHEN Stage 3 is displayed THEN the system SHALL show a battery positioned at grid coordinates (1, 4) to (1, 8)
5. WHEN Stage 3 is displayed THEN the system SHALL show two light bulbs positioned at (7, 3) to (9, 3) and (7, 11) to (9, 11)
6. WHEN Stage 3 is displayed THEN the system SHALL show L-shaped wires at positions (1, 4), (1, 10), (10, 4), and (10, 10)
7. WHEN Stage 3 is displayed THEN the system SHALL show straight wires connecting the circuit components in a series configuration
8. WHEN Stage 3 is displayed THEN the system SHALL show missing part indicators at positions (4, 4) to (6, 4), (4, 10) to (6, 10), (6, 6) to (6, 8), and (12, 6) to (12, 8)
9. WHEN Stage 3 circuit is evaluated THEN the system SHALL require ALL missing parts to be filled with conductors for both light bulbs to light up
10. WHEN Stage 3 has even one missing conductor or any insulator in the circuit path THEN the system SHALL keep both light bulbs off

### Requirement 22

**User Story:** As a child learning about series circuits, I want the Stage 3 circuit to demonstrate that all components must be connected in a single path, so that I understand how series circuits work differently from parallel circuits.

#### Acceptance Criteria

1. WHEN Stage 3 loads THEN the system SHALL center the entire series circuit layout within the 15x15 grid
2. WHEN Stage 3 is displayed THEN the system SHALL show continuous wire connections forming a single series path
3. WHEN Stage 3 wires are displayed THEN the system SHALL create a path that connects battery → first light bulb → second light bulb → back to battery
4. WHEN Stage 3 wires are displayed THEN the system SHALL show that electricity must flow through both light bulbs in sequence
5. WHEN items are placed in Stage 3 THEN the system SHALL maintain continuous wire connections between all conductive components
6. WHEN Stage 3 circuit is complete with all conductors THEN the system SHALL light up both bulbs simultaneously
7. WHEN Stage 3 circuit has any gap or insulator THEN the system SHALL keep both bulbs off to demonstrate series circuit behavior
8. WHEN Stage 3 circuit is complete THEN the system SHALL visually demonstrate how current flows through the entire series path

### Requirement 23

**User Story:** As a child who successfully completes Stage 3, I want to see educational information about series circuits in the success modal, so that I can learn about how series circuits work and their real-world applications.

#### Acceptance Criteria

1. WHEN I complete Stage 3 successfully THEN the system SHALL display the success modal with congratulatory content
2. WHEN the Stage 3 success modal is displayed THEN the system SHALL include a "What you learned" section
3. WHEN the "What you learned" section is shown THEN the system SHALL provide age-appropriate information about what series circuits are
4. WHEN the series circuit education is displayed THEN the system SHALL explain that series circuits have components connected in a single path
5. WHEN the series circuit education is displayed THEN the system SHALL explain that electricity must flow through all components in order
6. WHEN the series circuit education is displayed THEN the system SHALL explain that if one component fails, the entire circuit stops working
7. WHEN the series circuit education is displayed THEN the system SHALL mention real-world examples like old Christmas lights or flashlights
8. WHEN the series circuit education is displayed THEN the system SHALL compare series circuits to parallel circuits from Stage 2
9. WHEN the educational content is shown THEN the system SHALL use simple, child-friendly language appropriate for the target audience
10. WHEN the Stage 3 success modal is displayed THEN the system SHALL maintain the same congratulatory tone while adding the educational component
11. WHEN the "What you learned" section discusses series circuits THEN the system SHALL clearly define what a series circuit is using simple terms like "components connected one after another in a chain"
12. WHEN explaining series circuits THEN the system SHALL emphasize that all parts must work together for the circuit to function
13. WHEN the series circuit explanation is provided THEN the system SHALL include visual metaphors that children can understand, such as comparing it to a chain where if one link breaks, the whole chain fails

### Requirement 24

**User Story:** As a child learning about parallel circuits in Stage 4, I want to understand that completing only one path will light only one bulb, so that I can learn how parallel circuits allow independent operation of different branches.

#### Acceptance Criteria

1. WHEN I fill only the 2-cell missing part with a conductor in Stage 4 while leaving other missing parts unfilled or filled with insulators THEN the system SHALL light up only the left light bulb
2. WHEN only the left circuit path is complete in Stage 4 THEN the system SHALL keep the right light bulb switched off
3. WHEN only one parallel path is complete in Stage 4 THEN the system SHALL show electrical charges and current flow only through the completed left circuit path
4. WHEN only the left bulb is lit in Stage 4 THEN the system SHALL NOT display the success modal since not all light bulbs are switched on
5. WHEN only one bulb is lit in Stage 4 THEN the system SHALL demonstrate that parallel circuits allow independent operation of different branches
6. WHEN the left path is complete but the right path is incomplete in Stage 4 THEN the system SHALL show current flow from battery positive terminal through the left bulb circuit and back to battery negative terminal
7. WHEN only partial completion occurs in Stage 4 THEN the system SHALL provide visual feedback showing which circuit path is active and which is inactive
8. WHEN testing a partially complete Stage 4 circuit THEN the system SHALL accurately represent the electrical behavior of parallel circuits where each branch operates independently

### Requirement 25

**User Story:** As a child using the game on smaller screens where the item bank doesn't fit beside the grid area, I want to access items through a tabbed menu at the bottom of the grid area, so that I can still easily select and drag items to build circuits.

#### Acceptance Criteria

1. WHEN the screen size is too small to display the item bank beside the grid area THEN the system SHALL hide the side item bank
2. WHEN the side item bank is hidden THEN the system SHALL display a tabbed menu interface at the bottom of the grid area
3. WHEN the tabbed menu is displayed THEN the system SHALL show three tabs: "1-Cell Items", "2-Cell Items", and "3-Cell Items"
4. WHEN the tabbed menu loads THEN the system SHALL default to showing the "1-Cell Items" tab as active
5. WHEN I click on the "1-Cell Items" tab THEN the system SHALL display all 1-cell items (Copper Coin, Bottle Cap, Lego Brick, Pebble, Button)
6. WHEN I click on the "2-Cell Items" tab THEN the system SHALL display all 2-cell items (Metal Key, Paper Clip, Eraser, Rubber Band)
7. WHEN I click on the "3-Cell Items" tab THEN the system SHALL display all 3-cell items (Spoon, Metal Ruler, Popsicle Stick, Straw)
8. WHEN items are displayed in the tabbed menu THEN the system SHALL maintain the same visual representation and labeling as the side item bank
9. WHEN I drag items from the tabbed menu THEN the system SHALL provide the same drag-and-drop functionality as the side item bank
10. WHEN the tabbed menu is active THEN the system SHALL maintain all tooltip functionality for item identification
11. WHEN switching between tabs THEN the system SHALL preserve the current quantities of items in each category
12. WHEN the screen size changes to accommodate the side item bank THEN the system SHALL automatically switch back to the side item bank layout and hide the tabbed menu