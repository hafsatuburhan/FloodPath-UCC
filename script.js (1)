
"use strict";

// =============================================
// FLOODPATH UCC - CAMPUS ROUTE LAB
// Stack-based Depth-First Search (DFS)
// =============================================

const GRID_SIZE = 8;
const TOTAL_TILES = GRID_SIZE * GRID_SIZE;

// Each location has a short map label and a full name.
// Coordinates are illustrative grid positions, not official geography.
const landmarks = {
  "GATE": { name: "UCC Main Gate", row: 7, col: 0 },
  "LIB":  { name: "UCC Library", row: 1, col: 1 },
  "SCI":  { name: "Science Area", row: 2, col: 3 },
  "ADM":  { name: "Administration", row: 4, col: 1 },
  "QUAD": { name: "Central Quad", row: 3, col: 3 },
  "CAF":  { name: "Cafeteria", row: 4, col: 4 },
  "SPT":  { name: "Sports Field", row: 6, col: 2 },
  "RES":  { name: "Student Residence", row: 6, col: 5 },
  "AMA":  { name: "Amamoma", row: 7, col: 6 },
  "AYE":  { name: "Ayensu", row: 0, col: 6 }
};

const landmarkAt = new Map();
const floodTiles = new Set();
let discoveredRoute = [];
let selectedTile = null;
let editMode = false;
let lastStackDisplay = [];
let lastSearch = null;
let logEntries = [];

const mapGrid = document.getElementById("mapGrid");
const tileInfo = document.getElementById("tileInfo");
const stackDisplay = document.getElementById("stackDisplay");
const activityLog = document.getElementById("activityLog");

// Build a lookup from grid coordinates to landmark IDs.
Object.keys(landmarks).forEach(function (id) {
  const place = landmarks[id];
  landmarkAt.set(tileId(place.row, place.col), id);
});

// Convert row and column to a unique tile ID.
function tileId(row, col) {
  return row * GRID_SIZE + col;
}

// Convert a tile ID back to row and column.
function tilePosition(id) {
  return {
    row: Math.floor(id / GRID_SIZE),
    col: id % GRID_SIZE
  };
}

// Return the landmark ID at a tile, if any.
function landmarkIdAt(id) {
  return landmarkAt.has(id) ? landmarkAt.get(id) : null;
}

// Return the full readable name of a tile.
function tileName(id) {
  const landmarkId = landmarkIdAt(id);

  if (landmarkId) {
    return landmarks[landmarkId].name;
  }

  const position = tilePosition(id);
  return "Path tile — Row " + (position.row + 1) +
    ", Column " + (position.col + 1);
}

// Determine whether a tile is a landmark.
function isLandmark(id) {
  return landmarkAt.has(id);
}

// Get the current start and destination tile IDs.
function getStartId() {
  const id = document.getElementById("startSelect").value;
  const place = landmarks[id];
  return tileId(place.row, place.col);
}

function getEndId() {
  const id = document.getElementById("endSelect").value;
  const place = landmarks[id];
  return tileId(place.row, place.col);
}

// Return whether a tile is blocked by simulated flooding.
function isFlooded(id) {
  return floodTiles.has(id);
}

// =============================================
// MAP RENDERING
// =============================================

function renderMap() {
  mapGrid.innerHTML = "";

  const startId = getStartId();
  const endId = getEndId();

  for (let id = 0; id < TOTAL_TILES; id++) {
    const landmarkId = landmarkIdAt(id);
    const flooded = isFlooded(id);
    const onRoute = discoveredRoute.includes(id);

    const button = document.createElement("button");
    button.type = "button";
    button.className = "map-tile";
    button.dataset.tileId = String(id);

    // The label inside the tile is short.
    // The information panel shows the full location name.
    if (landmarkId) {
      button.textContent = landmarkId;
      button.classList.add("landmark");
    } else {
      button.textContent = flooded ? "!" : "·";
    }

    if (flooded) {
      button.classList.add("flooded");
    }

    if (onRoute) {
      button.classList.add("on-route");
    }

    if (id === startId) {
      button.classList.add("start-tile");
    }

    if (id === endId) {
      button.classList.add("end-tile");
    }

    if (id === selectedTile) {
      button.classList.add("selected-tile");
    }

    const status = getTileStatus(id);
    button.title = tileName(id) + " — " + status;
    button.setAttribute(
      "aria-label",
      tileName(id) + ". " + status +
      (id === startId ? ". Starting point." : "") +
      (id === endId ? ". Destination." : "")
    );

    button.addEventListener("click", function () {
      handleTileClick(id);
    });

    mapGrid.appendChild(button);
  }

  document.getElementById("floodCount").textContent = floodTiles.size;
}

function getTileStatus(id) {
  if (isFlooded(id)) {
    return "Blocked by simulated flooding";
  }

  if (id === getStartId()) {
    return "Starting point — route begins here";
  }

  if (id === getEndId()) {
    return "Destination — route ends here";
  }

  if (discoveredRoute.includes(id)) {
    return "Part of the discovered route";
  }

  if (isLandmark(id)) {
    return "Landmark tile — passable in this simulation";
  }

  return "Normal, passable path tile";
}

// =============================================
// TILE INFORMATION AND FLOOD EDITING
// =============================================

function showTileInfo(id, message) {
  selectedTile = id;

  const title = tileName(id);
  let status = getTileStatus(id);
  const position = tilePosition(id);

  if (message) {
    status = message;
  }

  tileInfo.innerHTML = "";

  const heading = document.createElement("strong");
  heading.textContent = title;

  const details = document.createElement("p");
  details.textContent =
    "Grid position: Row " + (position.row + 1) +
    ", Column " + (position.col + 1) +
    ". Status: " + status + ".";

  tileInfo.appendChild(heading);
  tileInfo.appendChild(details);
}

function handleTileClick(id) {
  selectedTile = id;

  if (!editMode) {
    showTileInfo(id);
    renderMap();
    return;
  }

  if (isLandmark(id)) {
    showTileInfo(
      id,
      "Landmark tiles cannot be flooded in this simulation. Select an ordinary path tile instead"
    );
    addLog("Tile inspection", tileName(id) +
      " is a landmark and cannot be flood-blocked.");
    renderMap();
    return;
  }

  if (id === getStartId() || id === getEndId()) {
    showTileInfo(
      id,
      "This is the selected start or destination. Change the route settings before blocking it"
    );
    renderMap();
    return;
  }

  if (floodTiles.has(id)) {
    floodTiles.delete(id);
    showTileInfo(id, "Flood block removed. This path tile is now passable");
    addLog("Flood cleared", tileName(id) + " is now passable.");
  } else {
    floodTiles.add(id);
    showTileInfo(id, "Simulated flood block added. Route search cannot pass through this tile");
    addLog("Flood simulated", tileName(id) + " has been blocked.");
  }

  clearRouteData(false);
  renderMap();
  updateRouteCards();
}

function setEditMode(enabled) {
  editMode = enabled;

  document.getElementById("inspectModeBtn")
    .classList.toggle("selected", !enabled);

  document.getElementById("editModeBtn")
    .classList.toggle("selected", enabled);

  if (enabled) {
    addLog("Map mode", "Flood editing enabled. Tap an ordinary path tile to block or unblock it.");
    if (selectedTile !== null) {
      showTileInfo(selectedTile, "Flood editing mode is active. Tap an ordinary path tile to edit it");
    } else {
      tileInfo.innerHTML =
        "<strong>Flood editing mode</strong><p>Tap an ordinary path tile to add or remove a simulated flood block. Landmark tiles are protected.</p>";
    }
  } else {
    addLog("Map mode", "Inspection mode enabled. Tap any tile to read its full name and status.");
    if (selectedTile !== null) {
      showTileInfo(selectedTile);
    } else {
      tileInfo.innerHTML =
        "<strong>Map tile information</strong><p>Tap a tile to see its full name and status.</p>";
    }
  }
}

// =============================================
// DFS ROUTE SEARCH USING A STACK
// =============================================

// Four-direction movement: up, right, down, left.
// Diagonal movement is not allowed.
function getNeighbors(id) {
  const position = tilePosition(id);
  const options = [
    [position.row - 1, position.col],
    [position.row, position.col + 1],
    [position.row + 1, position.col],
    [position.row, position.col - 1]
  ];

  const result = [];

  options.forEach(function (pair) {
    const row = pair[0];
    const col = pair[1];

    if (
      row >= 0 && row < GRID_SIZE &&
      col >= 0 && col < GRID_SIZE
    ) {
      result.push(tileId(row, col));
    }
  });

  return result;
}

// Search for a route with an explicit stack.
// Each stack entry stores a tile and the path used to reach it.
function findRouteDFS(startId, endId) {
  const stack = [{ id: startId, path: [startId] }];
  const visited = new Set([startId]);

  let pushes = 1;
  let pops = 0;
  let foundPath = null;
  const searchLog = [];

  searchLog.push(
    "PUSH " + tileName(startId) + " onto the stack."
  );

  while (stack.length > 0) {
    const current = stack.pop();
    pops++;

    searchLog.push("POP " + tileName(current.id) + " from the stack.");

    if (current.id === endId) {
      foundPath = current.path;
      searchLog.push("Destination reached: " + tileName(endId) + ".");
      break;
    }

    const neighbors = getNeighbors(current.id);

    // Reverse push order so the first direction in the list
    // is explored first when the stack uses LIFO.
    for (let i = neighbors.length - 1; i >= 0; i--) {
      const nextId = neighbors[i];

      if (visited.has(nextId) || isFlooded(nextId)) {
        continue;
      }

      visited.add(nextId);

      const newPath = current.path.concat(nextId);
      stack.push({
        id: nextId,
        path: newPath
      });

      pushes++;
      searchLog.push(
        "PUSH " + tileName(nextId) + " onto the stack."
      );
    }
  }

  if (!foundPath) {
    searchLog.push(
      "No route found. The destination may be cut off by flood blocks."
    );
  }

  return {
    path: foundPath,
    pushes: pushes,
    pops: pops,
    visited: visited.size,
    log: searchLog
  };
}

function runRouteSearch() {
  const startId = getStartId();
  const endId = getEndId();

  clearRouteData(false);
  selectedTile = null;

  if (startId === endId) {
    addLog("Route search", "Choose two different locations for the start and destination.");
    updateRouteCards();
    renderMap();
    return;
  }

  if (isFlooded(startId) || isFlooded(endId)) {
    addLog("Route search failed", "The start or destination is blocked. Reset the flood block or choose another location.");
    updateRouteCards();
    renderMap();
    return;
  }

  addLog("DFS started", "Searching from " + tileName(startId) +
    " to " + tileName(endId) + ".");

  const result = findRouteDFS(startId, endId);
  lastSearch = result;
  discoveredRoute = result.path || [];

  // Show the discovered route as a stack:
  // the destination appears at the top.
  lastStackDisplay = result.path ? result.path.slice().reverse() : [];

  result.log.slice(-30).forEach(function (entry) {
    addLog("DFS", entry);
  });

  if (result.path) {
    addLog(
      "Route found",
      "DFS reached " + tileName(endId) + " using " +
      result.path.length + " tiles. This is a valid route, not necessarily the shortest route."
    );
  } else {
    addLog(
      "No route",
      "DFS could not reach " + tileName(endId) +
      ". Try removing some flood blocks."
    );
  }

  renderMap();
  renderStack();
  updateRouteCards();
}

// =============================================
// STACK DISPLAY AND DASHBOARD STATS
// =============================================

function renderStack() {
  stackDisplay.innerHTML = "";

  if (lastStackDisplay.length === 0) {
    const empty = document.createElement("div");
    empty.className = "empty-stack";
    empty.textContent =
      "No route stack to display yet. Run DFS and check the exploration log.";
    stackDisplay.appendChild(empty);
  } else {
    lastStackDisplay.forEach(function (id, index) {
      const item = document.createElement("div");
      item.className = "stack-item";

      const name = document.createElement("span");
      name.textContent = tileName(id);

      const label = document.createElement("small");
      label.textContent = index === 0 ? "TOP" : "STACK";

      item.appendChild(name);
      item.appendChild(label);
      stackDisplay.appendChild(item);
    });
  }

  document.getElementById("pushCount").textContent =
    lastSearch ? lastSearch.pushes : 0;

  document.getElementById("popCount").textContent =
    lastSearch ? lastSearch.pops : 0;

  document.getElementById("visitedCount").textContent =
    lastSearch ? lastSearch.visited : 0;
}

function updateRouteCards() {
  const status = document.getElementById("routeStatus");
  const subtext = document.getElementById("routeSubtext");
  const length = document.getElementById("routeLength");

  if (!lastSearch) {
    status.textContent = "Not tested";
    subtext.textContent = "Choose locations to begin";
    length.textContent = "—";
    return;
  }

  if (lastSearch.path) {
    status.textContent = "Route found";
    subtext.textContent = "Destination is reachable";
    length.textContent = lastSearch.path.length;
  } else {
    status.textContent = "No route";
    subtext.textContent = "Try changing the flood blocks";
    length.textContent = "—";
  }
}

// =============================================
// RESET AND CLEAR ACTIONS
// =============================================

function clearRouteData(clearLogToo) {
  discoveredRoute = [];
  lastStackDisplay = [];
  lastSearch = null;

  renderStack();
  updateRouteCards();

  if (clearLogToo) {
    logEntries = [];
    renderLog();
  }
}

function clearRoute() {
  clearRouteData(false);
  renderMap();

  if (selectedTile !== null) {
    showTileInfo(selectedTile);
  }

  addLog("Route cleared", "The discovered route and stack summary have been cleared.");
}

function resetFloods() {
  floodTiles.clear();
  clearRouteData(false);
  renderMap();
  updateRouteCards();

  if (selectedTile !== null) {
    showTileInfo(selectedTile, "All flood blocks have been removed. This tile is now unblocked unless it is a landmark");
  }

  addLog("Map reset", "All simulated flood blocks have been removed.");
}

// =============================================
// EXPLORATION LOG
// =============================================

function addLog(category, message) {
  const time = new Date().toLocaleTimeString([], {
    hour: "2-digit",
    minute: "2-digit",
    second: "2-digit"
  });

  logEntries.unshift({
    time: time,
    category: category,
    message: message
  });

  // Keep the latest 60 messages.
  logEntries = logEntries.slice(0, 60);
  renderLog();
}

function renderLog() {
  activityLog.innerHTML = "";

  if (logEntries.length === 0) {
    const empty = document.createElement("p");
    empty.className = "log-empty";
    empty.textContent = "Ready. Choose locations and find a route to begin.";
    activityLog.appendChild(empty);
    return;
  }

  logEntries.forEach(function (entry) {
    const row = document.createElement("div");
    row.className = "log-entry";

    const mark = document.createElement("span");
    mark.className = "log-mark";
    mark.textContent = "›";

    const content = document.createElement("div");
    content.textContent =
      "[" + entry.time + "] " + entry.category + ": " + entry.message;

    row.appendChild(mark);
    row.appendChild(content);
    activityLog.appendChild(row);
  });
}

// =============================================
// EVENT LISTENERS
// =============================================

document.getElementById("inspectModeBtn")
  .addEventListener("click", function () {
    setEditMode(false);
  });

document.getElementById("editModeBtn")
  .addEventListener("click", function () {
    setEditMode(true);
  });

document.getElementById("findRouteBtn")
  .addEventListener("click", runRouteSearch);

document.getElementById("clearRouteBtn")
  .addEventListener("click", clearRoute);

document.getElementById("resetFloodsBtn")
  .addEventListener("click", resetFloods);

document.getElementById("clearLogBtn")
  .addEventListener("click", function () {
    logEntries = [];
    renderLog();
  });

// Refresh the map when the selected start or destination changes.
document.getElementById("startSelect")
  .addEventListener("change", function () {
    clearRouteData(false);
    renderMap();
    updateRouteCards();
    addLog("Route settings", "Starting location changed to " +
      landmarks[this.value].name + ".");
  });

document.getElementById("endSelect")
  .addEventListener("change", function () {
    clearRouteData(false);
    renderMap();
    updateRouteCards();
    addLog("Route settings", "Destination changed to " +
      landmarks[this.value].name + ".");
  });

// =============================================
// INITIALIZE THE APPLICATION
// =============================================

renderMap();
renderStack();
updateRouteCards();
renderLog();

addLog(
  "System ready",
  "FloodPath UCC is ready. Inspect tiles, simulate flood blocks, or run DFS."
);
