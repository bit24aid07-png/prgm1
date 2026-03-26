import heapq

# Initial and goal states
initial_state = (3, 3, 1)
goal_state = (0, 0, 0)

visited = set()

# Heuristic function
def heuristic(state):
    # Number of people remaining on left side
    return state[0] + state[1]

# Check if state is valid
def is_valid(m, c):
    if m < 0 or c < 0 or m > 3 or c > 3:
        return False

    # Missionaries eaten condition
    if m > 0 and c > m:
        return False

    m_right = 3 - m
    c_right = 3 - c

    if m_right > 0 and c_right > m_right:
        return False

    return True

# Generate next states
def successors(state):
    m, c, boat = state
    moves = [(1,0), (2,0), (0,1), (0,2), (1,1)]
    result = []

    for dm, dc in moves:
        if boat == 1:  # boat on left
            new_state = (m-dm, c-dc, 0)
        else:          # boat on right
            new_state = (m+dm, c+dc, 1)

        if is_valid(new_state[0], new_state[1]):
            result.append(new_state)

    return result

# Best First Search
def best_first_search():
    pq = []
    heapq.heappush(pq, (heuristic(initial_state), initial_state, []))

    while pq:
        _, current, path = heapq.heappop(pq)

        if current in visited:
            continue

        visited.add(current)
        path = path + [current]

        if current == goal_state:
            return path

        for next_state in successors(current):
            if next_state not in visited:
                heapq.heappush(pq,
                    (heuristic(next_state), next_state, path))

    return None

solution = best_first_search()

print("Solution Path:")
for step in solution:
    print(step)
