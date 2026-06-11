# 🎵 Java Data Graph — Spotify Songs Visualizer

Hand-written Java HTTP server using com.sun.net.httpserver, no external dependencies, that reads a Spotify dataset CSV, analyzes song data, and serves it as JSON to a live browser chart — no frameworks, no libraries, just Java + Chart.js.

---

##  Tech Stack

| Layer      | Technology                              |
|------------|-----------------------------------------|
| Server     | Java (`com.sun.net.httpserver`)         |
| Data       | CSV file read via `Scanner` + `FileOperator` |
| Frontend   | HTML + CSS + Chart.js (CDN)             |
| No external Java libraries |

---

##  Project Structure

```
├── Server.java          # HTTP server (port 8080), routes: /, /style.css, /code.js, /data
├── DataAnalyzer.java    # Parses CSV, computes stats, serializes to JSON
├── Song.java            # Song model with 20 fields + toJson()
├── FileOperator.java    # File utility (reads CSV/txt into ArrayList)
├── Country.java         # Country model (internet usage data — alternate dataset)
├── dataset.csv          # Spotify songs dataset
├── genres.txt           # Genre list (supplemental)
├── numbers.txt          # Integer list (used for binary search demo)
├── index.html           # Frontend: bar chart UI
├── style.css            # Dark theme, CSS variables, animations
└── code.js              # Fetch from /data → Chart.js bar chart (top 10)
```

---

## API Endpoints

| Endpoint     | Description                                      |
|--------------|--------------------------------------------------|
| `GET /`      | Serves `index.html`                              |
| `GET /style.css` | Serves stylesheet                            |
| `GET /code.js`   | Serves frontend JavaScript                   |
| `GET /data`  | Returns first 100 songs as JSON array            |
| `GET /stats` | (Stubbed — not yet implemented)                  |

### Sample `/data` response
```json
[
  {"name": "The Weeknd", "value": "0.714"},
  {"name": "Drake", "value": "0.832"},
  ...
]
```
> `name` = artist, `value` = danceability score

---

##  Frontend Behavior

- Fetches `/data` on page load
- Sorts songs by `value` descending, takes **top 10**
- Renders a **gradient bar chart** via Chart.js
- Shows error box if server is not running
- **Refresh Data** button re-fetches and redraws

---

##  DataAnalyzer Methods

| Method | Description |
|--------|-------------|
| `createSongs()` | Parses CSV into `ArrayList<Song>` |
| `findMinInstrumentalness()` | Lowest instrumentalness value |
| `findMaxInstrumentalness()` | Highest instrumentalness value |
| `findSumInstrumentalness()` | Sum of all instrumentalness values |
| `findAveInstrumentalness()` | Average (rounded to 2 decimal places) |
| `findMaxInstrumentalnessTrack()` | Track name with highest instrumentalness |
| `findMinInstrumentalnessTrack()` | Track name with lowest instrumentalness |
| `linearSearch()` | Search songs by track name |
| `binarySearch()` | Binary search on sorted integer list |
| `reverseList()` | Reverses ArrayList order |
| `toJSon()` | Serializes song list to JSON string |

---

## How to Run

```bash
# Compile all Java files
javac *.java

# Run the server
java Server

# Open in browser
http://localhost:8080
```

> Make sure `dataset.csv`, `index.html`, `style.css`, and `code.js` are in the **same directory** as the compiled classes.

---

##  Teaching Notes

This project demonstrates AP CS A concepts:
- `ArrayList` traversal and manipulation
- CSV file parsing with edge cases (quoted commas)
- Linear search and binary search
- Min / max / sum / average algorithms
- Object-oriented design (`Song`, `Country`, `FileOperator`)
- JSON serialization without external libraries
- Connecting Java backend to a browser frontend via HTTP
