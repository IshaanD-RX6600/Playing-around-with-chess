chess.js
Description:
chess.js is a TypeScript chess library for move generation/validation, piece placement/movement, and detecting check/checkmate/stalemate. It’s a headless library, meaning it doesn’t include a user interface, but it can be paired with libraries like chessboard.js for visualization.

Features
Move generation and validation.

Check/checkmate/stalemate detection.

Support for Forsyth-Edwards Notation (FEN) and Portable Game Notation (PGN).

Permissive and strict move parsers.

Works in Node.js and modern browsers.

Installation
Install via npm:

bash
Copy
npm install chess.js
Usage
Importing
ESM (Modern JavaScript):

javascript
Copy
import { Chess } from 'chess.js';
CommonJS:

javascript
Copy
const { Chess } = require('chess.js');
Example: Play a Random Game
javascript
Copy
import { Chess } from 'chess.js';

const chess = new Chess();

while (!chess.isGameOver()) {
  const moves = chess.moves();
  const move = moves[Math.floor(Math.random() * moves.length)];
  chess.move(move);
}

console.log(chess.pgn()); // Output the game in PGN format
Key Methods
chess.move(move): Make a move (supports SAN or object notation).

chess.ascii(): Print an ASCII representation of the board.

chess.fen(): Get the current position in FEN format.

chess.pgn(): Get the game in PGN format.

chess.isGameOver(): Check if the game has ended.

chess.load(fen): Load a position from a FEN string.

chess.loadPgn(pgn): Load a game from PGN.

Parsers
Permissive Parser: Handles non-standard move notations (e.g., Nf3, g1f3, Ng1-f3).

Strict Parser: Only accepts Standard Algebraic Notation (SAN).

Constants
Exported constants include:

Piece types: PAWN, KNIGHT, BISHOP, ROOK, QUEEN, KING.

Colors: WHITE, BLACK.

Starting FEN: DEFAULT_POSITION.

Integration with UI
chess.js is often paired with chessboard.js for visualization. Example:

javascript
Copy
import { Chess } from 'chess.js';
import Chessboard from 'chessboardjs';

const chess = new Chess();
const board = Chessboard('board', {
  position: chess.fen(),
  onDrop: (source, target) => {
    const move = chess.move({ from: source, to: target });
    if (move === null) return 'snapback'; // Illegal move
    board.position(chess.fen());
  },
});
