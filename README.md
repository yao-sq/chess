# Chess
### show legal moves 

if piece is of type bishop
    return [c_line(1, 1), c_line(-1,-1), c_line(1,-1), c_line(-1,1)]
if piece is of type knight
    return [avail(2,1), avail(2,-1), avail(-2,1), avail(-2,-1), avail(1,2), avail(1,-2), avail(-1,2), avail(-1,-2)]
if piece is of type pawn
    avail(0,1), avail(0,2) if not moved, is_opponent(1,(black ? 1 : -1)), is_opponent(-1, (black ? 1 : -1)), en_passant
    

    
c_line: line, stopping at the first piece or border; includes the edge/interrupting if avail

line: xStep, yStep  defines a line in a direction
    
avail: return the given position itself if the place is available - no same-color piece already there, within board boundaries

not moved: (white && on row 7) || (black && on row 2)

en_passant: ((-1, 0) | (1, 0)) is_opponent && pawn && it did the "2 move"

pawn did the "2 move":  last move was distance 2



#####

<body>
    <board>
        <row><cell id="1:1"><piece class="rook"></piece></cell></row>
    </board>
</body>