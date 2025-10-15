# Design Document

## Overview

The Conductor-Insulator Game is a web-based educational game built with Phaser.js that teaches children about electrical conductivity through interactive circuit building. The game features a drag-and-drop interface where players complete electrical circuits by selecting appropriate materials from an item bank and placing them in missing circuit segments.

## Architecture

### Game Structure
- **Three Simple Files**: HTML file with embedded CSS and JavaScript sections
- **Phaser.js Framework**: Handles game loop, input management, and rendering via CDN
- **Single Scene Architecture**: Main game scene with simple modal overlays
- **Simple Object Design**: Basic JavaScript objects for circuit components

### Core Systems
1. **Grid System**: Manages positioning and snapping of circuit components
2. **Drag-and-Drop System**: Handles item selection, dragging, placement validation, and removal
3. **Circuit Evaluation System**: Analyzes circuit paths and determines electrical flow
4. **Item Management System**: Manages item bank inventory and item properties
5. **Visual Connection System**: Renders continuous wire connections between components
6. **UI System**: Handles buttons, modals, and visual feedback

## Grid Expansion Design

### 15x15 Grid Layout
The expanded grid provides significantly more space for complex circuit designs while maintaining the educational focus:

- **Grid Dimensions**: 15 columns × 15 rows (increased from 12×8)
- **Canvas Size**: 900px × 900px (15 × 60px cells)
- **Component Positioning**: Battery and bulb repositioned to center rows for better visual balance
- **Circuit Complexity**: Support for multiple parallel paths, branching circuits, and creative layouts

### Responsive Design Considerations
```javascript
// Adaptive canvas sizing for different screen sizes
const getOptimalCellSize = () => {
  const maxWidth = Math.min(window.innerWidth * 0.6, 900);
  const maxHeight = Math.min(window.innerHeight * 0.7, 900);
  return Math.min(maxWidth / 15, maxHeight / 15, 60);
};

// Dynamic grid configuration
const gameConfig = {
  width: 15 * cellSize,
  height: 15 * cellSize,
  gridWidth: 15,
  gridHeight: 15
};
```

### Enhanced Circuit Layouts
The larger grid enables:
- **Multi-path circuits**: Parallel conductors and alternative routes
- **Complex branching**: Circuits that split and rejoin
- **Educational scenarios**: More realistic electrical system representations
- **Creative freedom**: Students can design their own circuit layouts

## Components and Interfaces

### Simple Game Objects
```javascript
// Simple object structures instead of classes
const gameState = {
  grid: [], // 2D array for grid positions (15x15)
  gridWidth: 15, // Expanded from 12
  gridHeight: 15, // Expanded from 8
  itemBank: [], // Available items
  placedItems: [], // Items placed on grid
  battery: { x: 2, y: 7, type: 'battery' }, // Repositioned for center
  bulb: { x: 12, y: 7, type: 'bulb', isLit: false }, // Repositioned for center
  gaps: [
    // More gaps for complex circuits
    { x: 5, y: 6 }, { x: 7, y: 6 }, { x: 9, y: 6 }, // Top path
    { x: 9, y: 8 }, { x: 7, y: 8 }, { x: 5, y: 8 }  // Bottom path
  ]
};

// Simple functions instead of classes
function createItem(type, conductive, color) {
  return {
    type: type,
    conductive: conductive,
    color: color,
    sprite: null,
    placed: false
  };
}

function initializeGame() {
  // Set up grid, item bank, and initial circuit
}

function testCircuit() {
  // Simple path finding to check if circuit is complete
}
```

## Data Models

### Item Bank Configuration
```javascript
const ITEM_BANK_CONFIG = [
  {
    id: 'copper_wire',
    name: 'Copper Wire',
    type: 'conductor',
    conductive: true,
    size: { width: 1, height: 1 },
    color: 0xCD7F32,
    quantity: 5
  },
  {
    id: 'rubber_block',
    name: 'Rubber',
    type: 'insulator',
    conductive: false,
    size: { width: 1, height: 1 },
    color: 0x2F2F2F,
    quantity: 3
  },
  {
    id: 'metal_rod',
    name: 'Metal Rod',
    type: 'conductor',
    conductive: true,
    size: { width: 2, height: 1 },
    color: 0xC0C0C0,
    quantity: 2
  }
];
```

### Simple Circuit Evaluation
```javascript
function findCircuitPath(startX, startY, endX, endY, grid) {
  // Simple breadth-first search using basic arrays
  const queue = [{x: startX, y: startY}];
  const visited = [];
  
  while (queue.length > 0) {
    const current = queue.shift();
    // Check adjacent cells for conductive path
  }
  
  return false; // No complete path found
}

function evaluateCircuit() {
  // Check if there's a complete conductive path from battery to bulb
  const hasPath = findCircuitPath(
    gameState.battery.x + 1, gameState.battery.y,
    gameState.battery.x - 1, gameState.battery.y,
    gameState.grid
  );
  
  gameState.bulb.isLit = hasPath;
  return hasPath;
}
```

## Item Removal System

### Drag-Based Removal
```javascript
function handleItemDrag(item, pointer) {
  if (item.placed) {
    // Check if dragging away from original position
    const distance = Phaser.Math.Distance.Between(
      item.originalX, item.originalY,
      pointer.x, pointer.y
    );
    
    if (distance > REMOVAL_THRESHOLD) {
      // Mark for removal and return to bank
      removeItemFromCircuit(item);
      returnItemToBank(item);
    }
  }
}

function removeItemFromCircuit(item) {
  // Clear grid position
  gameState.grid[item.gridY][item.gridX] = null;
  
  // Update placed items array
  gameState.placedItems = gameState.placedItems.filter(i => i !== item);
  
  // Reset item state
  item.placed = false;
  item.gridX = -1;
  item.gridY = -1;
}
```

### Visual Feedback for Removal
- **Drag Distance Indicator**: Visual cue when item is being dragged far enough for removal
- **Return Animation**: Smooth animation returning item to bank
- **Grid Clear Effect**: Brief highlight of cleared grid position

## Visual Connection System

### Dynamic Wire Rendering
```javascript
function updateWireConnections() {
  // Clear existing connection graphics
  clearConnectionGraphics();
  
  // For each placed conductive item, draw connections to adjacent components
  gameState.placedItems.forEach(item => {
    if (item.conductive && item.placed) {
      drawConnectionsForItem(item);
    }
  });
  
  // Draw connections from battery and to bulb
  drawBatteryConnections();
  drawBulbConnections();
}

function drawConnectionsForItem(item) {
  const adjacentPositions = getAdjacentPositions(item.gridX, item.gridY);
  
  adjacentPositions.forEach(pos => {
    const adjacentItem = getItemAtPosition(pos.x, pos.y);
    if (adjacentItem && (adjacentItem.conductive || adjacentItem.type === 'wire')) {
      drawWireConnection(item, adjacentItem);
    }
  });
}

function drawWireConnection(fromItem, toItem) {
  const graphics = scene.add.graphics();
  graphics.lineStyle(4, 0xCD7F32); // Copper wire color
  
  const fromPos = gridToWorld(fromItem.gridX, fromItem.gridY);
  const toPos = gridToWorld(toItem.gridX, toItem.gridY);
  
  // Draw connecting wire with proper endpoints
  graphics.moveTo(fromPos.x, fromPos.y);
  graphics.lineTo(toPos.x, toPos.y);
  graphics.strokePath();
  
  // Store reference for cleanup
  gameState.connectionGraphics.push(graphics);
}
```

### Connection Validation
- **Continuous Path Check**: Ensure all connections form unbroken electrical path
- **Terminal Alignment**: Verify proper connection to battery terminals and bulb
- **Gap Bridging**: Show how placed items bridge the circuit gaps

## Reset System Enhancement

### Complete Game Reset
```javascript
function resetGame() {
  // Remove all placed items from circuit
  gameState.placedItems.forEach(item => {
    removeItemFromCircuit(item);
    returnItemToBank(item);
  });
  
  // Clear all connection graphics
  clearConnectionGraphics();
  
  // Reset bulb state
  updateLightBulb(false);
  
  // Reset item bank quantities
  resetItemBankQuantities();
  
  // Clear feedback messages
  clearFeedback();
  
  // Redraw base circuit components
  redrawBaseCircuit();
}

function resetItemBankQuantities() {
  // Restore original quantities for each item type
  gameState.itemBank.forEach(item => {
    item.inBank = true;
    item.placed = false;
    // Reset visual state in HTML
    updateItemBankDisplay(item);
  });
}
```

## Error Handling

### Input Validation
- **Invalid Drop Zones**: Items dropped outside valid grid positions return to item bank
- **Overlapping Components**: Prevent placement on occupied grid cells
- **Size Constraints**: Ensure multi-cell items fit within grid boundaries

### Circuit Evaluation Errors
- **Incomplete Circuits**: Handle circuits with gaps gracefully
- **Multiple Paths**: Evaluate all possible current paths
- **Component Failures**: Handle missing or corrupted component data

### User Experience Errors
- **Drag State Recovery**: Reset drag state if interaction is interrupted
- **Visual Feedback**: Clear indication of invalid actions
- **Performance**: Limit evaluation frequency to prevent lag

## Short Circuit Detection System

### Short Circuit Logic
```javascript
function detectShortCircuit() {
  // Check for short circuit condition in Stage 2
  if (gameState.currentStage !== 2) return false;
  
  // Check if conductor is placed in the critical 3-slot position (6,6) to (6,8)
  const criticalPositions = [{x: 6, y: 6}, {x: 6, y: 7}, {x: 6, y: 8}];
  const hasConductorInCriticalPath = criticalPositions.every(pos => {
    const item = getItemAtPosition(pos.x, pos.y);
    return item && item.conductive;
  });
  
  if (hasConductorInCriticalPath) {
    // Check if this creates a direct path bypassing the bulb
    const shortCircuitPath = findDirectBatteryPath();
    return shortCircuitPath.length > 0;
  }
  
  return false;
}

function findDirectBatteryPath() {
  // Find path from battery + terminal to battery - terminal that bypasses bulb
  const startPos = {x: gameState.battery.x + 1, y: gameState.battery.y};
  const endPos = {x: gameState.battery.x - 1, y: gameState.battery.y};
  
  return findPathExcludingBulb(startPos, endPos);
}
```

### Short Circuit Visual Feedback
```javascript
function displayShortCircuitFeedback() {
  // Show red current flow animation
  animateCurrentFlow({
    path: getShortCircuitPath(),
    color: 0xFF0000, // Red color for danger
    speed: 2.0, // Faster animation to show high current
    particles: true
  });
  
  // Keep bulb off
  updateLightBulb(false);
  
  // Show warning modal
  showShortCircuitModal();
}

function showShortCircuitModal() {
  const modalContent = {
    title: "⚠️ Short Circuit Detected!",
    message: `
      <p>Oops! You've created a short circuit. The electricity is taking a shortcut and bypassing the light bulb!</p>
      
      <h4>What is a Short Circuit?</h4>
      <p>A short circuit happens when electricity finds an easier path than the one we want it to take. Instead of flowing through the light bulb, it's going directly from the battery's + side to the - side.</p>
      
      <h4>Why is this a problem?</h4>
      <p>• The light bulb won't work because electricity isn't flowing through it</p>
      <p>• Too much electricity flows too fast, which can be dangerous</p>
      <p>• In real life, this could damage equipment or cause fires</p>
      
      <h4>How to fix it:</h4>
      <p>• Make sure electricity has to flow through the light bulb</p>
      <p>• Use insulators to block unwanted paths</p>
      <p>• Check that your circuit follows the intended path</p>
    `,
    buttons: [
      { text: "Try Again", action: "close" },
      { text: "Reset Circuit", action: "reset" }
    ]
  };
  
  createModal(modalContent);
}
```

### Enhanced Circuit Evaluation
```javascript
function evaluateCircuitWithShortCheck() {
  // First check for short circuit
  if (detectShortCircuit()) {
    gameState.circuitState = 'short_circuit';
    displayShortCircuitFeedback();
    return false;
  }
  
  // Normal circuit evaluation
  const hasValidPath = findCircuitPath(
    gameState.battery.x + 1, gameState.battery.y,
    gameState.bulb.x, gameState.bulb.y,
    gameState.grid
  );
  
  if (hasValidPath) {
    gameState.circuitState = 'complete';
    gameState.bulb.isLit = true;
    displaySuccessFeedback();
    return true;
  } else {
    gameState.circuitState = 'incomplete';
    gameState.bulb.isLit = false;
    return false;
  }
}
```

## Stage 3: Series Circuit Design

### Series Circuit Layout
Stage 3 introduces a more complex series circuit with dual light bulbs to teach students about series connections:

```
Grid Layout (15x15):
   0 1 2 3 4 5 6 7 8 9 10 11 12 13 14
0  . . . . . . . . . . .  .  .  .  .
1  . . . . . . . . . . .  .  .  .  .
2  . . . . . . . . . . .  .  .  .  .
3  . . . . . . . O O O .  .  .  .  .
4  . L W W M M W O O O W  W  L  .  .
5  . W . . . . . O O O .  .  W  .  .
6  . B . . . . . . . . .  .  M  .  .
7  . B . . . . . . . . .  .  M  .  .
8  . B . . . . . . . . .  .  M  .  .
9  . W . . . . . O O O .  .  W  .  .
10 . L W W M W W O O O W  W  L  .  .
11 . . . . . . . O O O .  .  .  .  .
12 . . . . . . . . . . .  .  .  .  .
13 . . . . . . . . . . .  .  .  .  .
14 . . . . . . . . . . .  .  .  .  .

Legend:
. = Empty Grid Cell
L = L-shaped wire
B = Battery
O = Light Bulb
W = Straight Wire
M = Missing Part Indicator
```

### Series Circuit Configuration
```javascript
const STAGE_3_CONFIG = {
  title: "Stage 3: Series Circuit",
  battery: { x: 1, y: 6, width: 1, height: 3 },
  lightBulbs: [
    { x: 7, y: 3, width: 3, height: 1, id: 'bulb1' },
    { x: 7, y: 11, width: 3, height: 1, id: 'bulb2' }
  ],
  wires: [
    // L-shaped wires
    { x: 1, y: 4, type: 'L-wire', rotation: 0 },
    { x: 1, y: 10, type: 'L-wire', rotation: 270 },
    { x: 10, y: 4, type: 'L-wire', rotation: 90 },
    { x: 10, y: 10, type: 'L-wire', rotation: 180 },
    
    // Straight wires
    { x: 2, y: 4, type: 'straight-wire' },
    { x: 3, y: 4, type: 'straight-wire' },
    { x: 7, y: 4, type: 'straight-wire' },
    { x: 11, y: 4, type: 'straight-wire' },
    { x: 12, y: 4, type: 'straight-wire' },
    
    { x: 2, y: 10, type: 'straight-wire' },
    { x: 3, y: 10, type: 'straight-wire' },
    { x: 7, y: 10, type: 'straight-wire' },
    { x: 11, y: 10, type: 'straight-wire' },
    { x: 12, y: 10, type: 'straight-wire' },
    
    { x: 1, y: 5, type: 'straight-wire' },
    { x: 1, y: 9, type: 'straight-wire' },
    { x: 12, y: 5, type: 'straight-wire' },
    { x: 12, y: 9, type: 'straight-wire' }
  ],
  missingParts: [
    { x: 4, y: 4, width: 3, height: 1 }, // Top horizontal gap
    { x: 4, y: 10, width: 3, height: 1 }, // Bottom horizontal gap
    { x: 6, y: 6, width: 1, height: 3 }, // Left vertical gap
    { x: 12, y: 6, width: 1, height: 3 } // Right vertical gap
  ]
};
```

### Series Circuit Evaluation Logic
```javascript
function evaluateSeriesCircuit() {
  // For series circuits, ALL gaps must be filled with conductors
  const allGapsFilled = gameState.missingParts.every(gap => {
    return isGapFilledWithConductor(gap);
  });
  
  if (!allGapsFilled) {
    // Turn off both bulbs if any gap is unfilled or has insulator
    gameState.lightBulbs.forEach(bulb => bulb.isLit = false);
    return false;
  }
  
  // Check for complete series path from battery through both bulbs
  const seriesPath = findSeriesPath();
  const isComplete = seriesPath.includesBothBulbs && seriesPath.isComplete;
  
  // Both bulbs light up simultaneously in series
  gameState.lightBulbs.forEach(bulb => bulb.isLit = isComplete);
  
  return isComplete;
}

function findSeriesPath() {
  // Find path that goes: Battery → Bulb1 → Bulb2 → Battery
  // or: Battery → Bulb2 → Bulb1 → Battery
  const startPos = { x: gameState.battery.x + 1, y: gameState.battery.y + 1 };
  const endPos = { x: gameState.battery.x - 1, y: gameState.battery.y + 1 };
  
  const path = findPathThroughBothBulbs(startPos, endPos);
  
  return {
    isComplete: path.length > 0,
    includesBothBulbs: path.includesBulb1 && path.includesBulb2,
    path: path
  };
}
```

### Educational Content for Stage 3
```javascript
const STAGE_3_EDUCATION = {
  title: "What you learned about Series Circuits:",
  content: [
    "🔗 Series circuits connect components in a single path",
    "⚡ Electricity must flow through ALL components in order",
    "💡 If one component breaks, the whole circuit stops working",
    "🎄 Examples: Old Christmas lights, flashlights, some car headlights",
    "🔄 Different from parallel circuits where components have separate paths",
    "🔧 Series circuits are simpler but less reliable than parallel circuits"
  ]
};
```

## Testing Strategy

### Manual Testing Approach
1. **Basic Functionality**: Test drag-and-drop, circuit evaluation, and success modal
2. **Game Flow**: Verify complete gameplay from start to successful circuit completion
3. **Educational Value**: Ensure the game clearly demonstrates conductor vs insulator behavior
4. **Short Circuit Testing**: Verify short circuit detection and appropriate warning messages
5. **Safety Education**: Confirm age-appropriate explanations of electrical safety concepts
6. **Series Circuit Testing**: Verify that both bulbs light up only when all gaps are filled with conductors
7. **Stage Progression**: Test progression from Stage 2 to Stage 3 and educational content display
8. **Browser Compatibility**: Test in major browsers (Chrome, Firefox, Safari, Edge)

## Visual Design

### Color Scheme
- **Conductors**: Metallic colors (copper, silver, gold)
- **Insulators**: Non-metallic colors (black rubber, brown wood)
- **Circuit Flow**: Animated particles or glowing effects for active circuits
- **Grid**: Subtle background grid lines for alignment guidance

### Layout
```
┌─────────────────────────────────────────────────────────┐
│  Game Title                                             │
├─────────────────────────────────┬───────────────────────┤
│                                 │   Item Bank           │
│      Expanded Playing Field     │  ┌─────┬─────┬─────┐  │
│       (15x15 Grid Circuit)      │  │ Cu  │ Rb  │ Mt  │  │
│                                 │  └─────┴─────┴─────┘  │
│  [Battery] ~~~ [Gap] ~~~ [Bulb] │  ┌─────┬─────┬─────┐  │
│     More space for complex      │  │ Wd  │ Al  │ Pl  │  │
│      circuit designs            │  └─────┴─────┴─────┘  │
├─────────────────────────────────┴───────────────────────┤
│                    [Test Circuit]                       │
└─────────────────────────────────────────────────────────┘
```

### Animation and Feedback
- **Drag Preview**: Semi-transparent item follows cursor during drag
- **Valid Drop Zones**: Highlight compatible gaps when dragging
- **Circuit Flow**: Animated current flow when circuit is complete
- **Success Animation**: Bulb glow effect and particle effects
- **Modal Transitions**: Smooth fade-in for success modal
- **Removal Feedback**: Visual indication when dragging items away for removal
- **Connection Visualization**: Dynamic wire rendering to show continuous electrical paths