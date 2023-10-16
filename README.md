# UML DESIGNS

## Class Diagram

```
classDiagram
    class ChessGame {
        board: Board
        startGame()
        movePiece(from: Square, to: Square)
    }
    class Board {
        squares: Square[8][8]
        pieces: List[Piece]
        initializeBoard()
        getSquareAtPosition(x: int, y: int): Square
    }
    class Square {
        x: int
        y: int
        piece: Piece
        isHighlighted: bool
        setPiece(piece: Piece)
        removePiece(): Piece
        highlight()
        unhighlight()
    }
    class Piece {
        color: String (White/Black)
        icon: Image
        moveTo(square: Square)
    }
    ChessGame "1" *-- "1" Board: uses
    Board "1" *-- "8x8" Square: has
    Square "1" o-- "0..1" Piece: can have
```
![Class Diagram](https://github.com/unko-chan/chess_oop/blob/main/class.png?raw=true)

## Sequence Diagram

```
sequenceDiagram
    participant Player
    participant ChessGame
    participant Board
    participant Square
    Player->>ChessGame: Clicks on a square containing a piece
    activate ChessGame
    ChessGame->>Board: getSquareAtPosition()
    activate Board
    Board-->>ChessGame: Return Square with the piece
    deactivate Board
    ChessGame->>Square: highlight()
    activate Square
    Square-->>ChessGame: Square is highlighted
    deactivate Square
    Player->>ChessGame: Clicks on another free square
    ChessGame->>Board: getSquareAtPosition() again
    activate Board
    Board-->>ChessGame: Return destination Square
    deactivate Board
    ChessGame->>ChessGame: movePiece(from, to)
    ChessGame->>Square: Remove piece from first square
    ChessGame->>Square: Place piece on destination square
    deactivate ChessGame
```

![Sequence Diagram](https://github.com/unko-chan/chess_oop/blob/main/sequence.png?raw=true)


## Collaboration Diagram

```
@startuml

object "ChessGame" as ChessGame
object "Board" as Board
object "Piece" as Piece
object "Square" as Square
object "Player" as Player

ChessGame --> Board : uses
Board --> Square : has-a
Square --> Piece : can have 0..1

Player --> ChessGame : Clicks on a square containing a piece
ChessGame --> Board : getSquareAtPosition()
Board --> ChessGame : Return Square with the piece
ChessGame --> Square : highlight()
Player --> ChessGame : Clicks on another free square
ChessGame --> Board : getSquareAtPosition() again
Board --> ChessGame : Return destination Square
ChessGame --> Square : Remove piece from first square
ChessGame --> Square : Place piece on destination square

@enduml
```

![Collaboration Diagram](https://github.com/unko-chan/chess_oop/blob/main/collaboration.png?raw=true)
