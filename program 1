# Water Jug Problem using Depth First Search

jug1_capacity = int(input("Enter capacity of Jug 1: "))
jug2_capacity = int(input("Enter capacity of Jug 2: "))
target = int(input("Enter target amount of water: ")) 

visited = set()
path = []

def dfs(a, b):
    # Goal condition
    if a == target or b == target:
        path.append((a, b))
        return True

    if (a, b) in visited:
        return False

    visited.add((a, b))
    path.append((a, b))

    next_states = []
    # Fill Jug 1
    next_states.append((jug1_capacity, b))
    # Fill Jug 2
    next_states.append((a, jug2_capacity))
    # Empty Jug 1
    next_states.append((0, b))
    # Empty Jug 2
    next_states.append((a, 0))
    # Pour Jug 1 -> Jug 2
    pour = min(a, jug2_capacity - b)
    next_states.append((a - pour, b + pour))
    # Pour Jug 2 -> Jug 1
    pour = min(b, jug1_capacity - a)
    next_states.append((a + pour, b - pour))

    for state in next_states:
        if state not in visited:
            if dfs(state[0], state[1]):
                return True

    path.pop()
    return False

dfs(0, 0)
print("Solution Path:")
for step in path:
    print(step)
