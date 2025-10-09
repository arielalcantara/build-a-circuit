# Requirements Document

## Introduction

This feature involves creating an educational game for children to learn about electrical conductors and insulators through interactive circuit building. The game uses a grid-based playing field where players drag and drop materials to complete electrical circuits, with immediate feedback on whether their solutions work correctly based on real electrical principles.

## Requirements

### Requirement 1

**User Story:** As a child learning about electricity, I want to see a grid-based playing field with a partially completed circuit, so that I can understand the basic structure of electrical circuits.

#### Acceptance Criteria

1. WHEN the game loads THEN the system SHALL display a grid-based playing field
2. WHEN the playing field is displayed THEN the system SHALL show a light bulb, battery, and pre-placed wires
3. WHEN the circuit is displayed THEN the system SHALL show missing gaps of varying sizes that need to be filled
4. WHEN the circuit is displayed THEN the system SHALL ensure the pre-placed wires guide toward a logical solution

### Requirement 2

**User Story:** As a child learning about materials, I want to see an item bank with different conductor and insulator materials, so that I can choose appropriate materials to complete the circuit.

#### Acceptance Criteria

1. WHEN the game loads THEN the system SHALL display an item bank beside the playing field
2. WHEN the item bank is displayed THEN the system SHALL show items of varying sizes
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

**User Story:** As a user accessing this educational game, I want it to run in a web browser using a single HTML file, so that it's easy to access and share.

#### Acceptance Criteria

1. WHEN the game is developed THEN the system SHALL be built using Phaser.js framework
2. WHEN the game is packaged THEN the system SHALL be contained in a single HTML file
3. WHEN the HTML file is opened in a browser THEN the system SHALL load and run the complete game
4. WHEN the game runs THEN the system SHALL not require external image files for basic functionality