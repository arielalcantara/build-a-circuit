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

## Components and Interfaces

### Simple Game Objects
```javascript
// Simple object structures instead of classes
const gameState = {
  grid: [], // 2D array for grid positions
  itemBank: [], // Available items
  placedItems: [], // Items placed on grid
  battery: { x: 1, y: 3, type: 'battery' },
  bulb: { x: 8, y: 3, type: 'bulb', isLit: false },
  gaps: [{ x: 4, y: 3 }, { x: 6, y: 3 }] // Missing circuit parts
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

## Testing Strategy

### Manual Testing Approach
1. **Basic Functionality**: Test drag-and-drop, circuit evaluation, and success modal
2. **Game Flow**: Verify complete gameplay from start to successful circuit completion
3. **Educational Value**: Ensure the game clearly demonstrates conductor vs insulator behavior
4. **Browser Compatibility**: Test in major browsers (Chrome, Firefox, Safari, Edge)

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
│         Playing Field           │  ┌─────┬─────┬─────┐  │
│      (Grid-based Circuit)       │  │ Cu  │ Rb  │ Mt  │  │
│                                 │  └─────┴─────┴─────┘  │
│  [Battery] ~~~ [Gap] ~~~ [Bulb] │  ┌─────┬─────┬─────┐  │
│                                 │  │ Wd  │ Al  │ Pl  │  │
│                                 │  └─────┴─────┴─────┘  │
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