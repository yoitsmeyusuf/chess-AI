import chess
import chess.uci

# Set up the board and engine
board = chess.Board()
engine = chess.uci.popen_engine("/path/to/engine")
engine.uci()

# Function to evaluate a board position using the chess engine
def evaluate_board(board):
    engine.position(board)
    return engine.go(movetime=200).bestmove

# Minimax function
def minimax(board, depth, alpha, beta, maximizing_player):
    if depth == 0 or board.is_game_over():
        return evaluate_board(board), None
    
    if maximizing_player:
        best_value = -float("inf")
        best_move = None
        for move in board.legal_moves:
            board.push(move)
            value, _ = minimax(board, depth - 1, alpha, beta, False)
            board.pop()
            if value > best_value:
                best_value = value
                best_move = move
            alpha = max(alpha, best_value)
            if alpha >= beta:
                break
        return best_value, best_move
    else:
        best_value = float("inf")
        best_move = None
        for move in board.legal_moves:
            board.push(move)
            value, _ = minimax(board, depth - 1, alpha, beta, True)
            board.pop()
            if value < best_value:
                best_value = value
                best_move = move
            beta = min(beta, best_value)
            if alpha >= beta:
                break
        return best_value, best_move

# Main loop
while not board.is_game_over():
    # Get the best move from the AI
    value, move = minimax(board, 2, -float("inf"), float("inf"), True)
    
    # Make the move
    board.push(move)
    
    # Print the board
    print(board)
    
    # Check if the game is over
    if board.is_game_over():
        break
    
    # Get the player's move
    move = input("Enter your move: ")
    board.push_uci(move)
    
# Print the final result
result = board.result()
if result == "1-0":
    print("White wins!")
elif result == "0-1":
    print("Black wins!")
else:
    print("It's a draw.")
