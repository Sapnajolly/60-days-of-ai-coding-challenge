# Day 20: Build an AI Face Puzzle Game

**Theme:** Phase 3 — AI-Powered App Development & Interactive Experiences  
**Focus:** Learn how to use Claude as a Front-End Game Developer

## What I Built
A fully functional Face Puzzle Game using Claude AI that:
- Uses webcam integration with `getUserMedia()`
- Captures your own photo and converts it into puzzle pieces
- Supports drag-and-drop mechanics
- Tracks timer and move count
- Saves top 5 best scores using `localStorage`
- Supports 3 difficulty levels (3×3, 4×4, 5×5)

## Key Learnings
- **Webcam API**: `navigator.mediaDevices.getUserMedia()` for camera access
- **Canvas API**: Drawing and slicing images into grid pieces
- **Drag & Drop**: HTML5 drag events for piece swapping
- **localStorage**: Persisting leaderboard scores across sessions
- **Game Logic**: Win detection when all pieces are in correct positions

## Claude Prompt Used
*"You are an expert front-end developer. Build me a complete, fully working face puzzle game as a single self-contained HTML file..."*

## Tools Used
- Claude AI (claude.ai)
- HTML5 Canvas API
- WebRTC / getUserMedia
- Vanilla JavaScript (no frameworks)
