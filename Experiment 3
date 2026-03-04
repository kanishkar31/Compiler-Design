# ==========================================================
# Lab 3: Conversion of NFA to DFA
# Subject: Compiler Design Laboratory
# Method: Subset Construction Algorithm
# ==========================================================

from collections import defaultdict, deque

# Function to calculate epsilon closure
def epsilon_closure(states, transitions):
    stack = list(states)
    closure = set(states)

    while stack:
        state = stack.pop()
        if (state, 'ε') in transitions:
            for next_state in transitions[(state, 'ε')]:
                if next_state not in closure:
                    closure.add(next_state)
                    stack.append(next_state)
    return closure


# Function to move from a set of states on a symbol
def move(states, symbol, transitions):
    result = set()
    for state in states:
        if (state, symbol) in transitions:
            result.update(transitions[(state, symbol)])
    return result


def nfa_to_dfa(states, symbols, transitions, start_state, final_states):
    dfa_states = []
    dfa_transitions = {}
    dfa_final_states = set()

    # Start state = epsilon closure of NFA start state
    start_closure = frozenset(epsilon_closure({start_state}, transitions))
    queue = deque([start_closure])
    dfa_states.append(start_closure)

    while queue:
        current = queue.popleft()

        for symbol in symbols:
            if symbol == 'ε':
                continue

            move_result = move(current, symbol, transitions)
            closure = frozenset(epsilon_closure(move_result, transitions))

            if not closure:
                continue

            dfa_transitions[(current, symbol)] = closure

            if closure not in dfa_states:
                dfa_states.append(closure)
                queue.append(closure)

    # Find DFA final states
    for dfa_state in dfa_states:
        if any(state in final_states for state in dfa_state):
            dfa_final_states.add(dfa_state)

    return dfa_states, dfa_transitions, start_closure, dfa_final_states


def main():
    print("======================================")
    print("   Compiler Design Lab - Lab 3")
    print("   NFA to DFA Conversion")
    print("   (Subset Construction Method)")
    print("======================================\n")

    n = int(input("Enter number of NFA states: "))
    states = [input(f"Enter state {i+1}: ") for i in range(n)]

    symbols = input("Enter input symbols (space separated, exclude ε): ").split()

    t = int(input("Enter number of transitions: "))
    transitions = defaultdict(list)

    print("\nEnter transitions in the format: from_state symbol to_state")
    for _ in range(t):
        s, sym, d = input().split()
        transitions[(s, sym)].append(d)

    start_state = input("\nEnter start state: ")
    final_states = set(input("Enter final states (space separated): ").split())

    dfa_states, dfa_transitions, dfa_start, dfa_finals = nfa_to_dfa(
        states, symbols, transitions, start_state, final_states
    )

    print("\n========== DFA STATES ==========")
    for i, state in enumerate(dfa_states):
        print(f"D{i} = {set(state)}")

    print("\n========== DFA TRANSITION TABLE ==========")
    for (state, symbol), next_state in dfa_transitions.items():
        print(f"{set(state)} -- {symbol} --> {set(next_state)}")

    print("\nDFA Start State:", set(dfa_start))

    print("DFA Final States:")
    for fs in dfa_finals:
        print(set(fs))


if __name__ == "__main__":
    main()
