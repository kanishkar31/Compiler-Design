# =========================================================
# Lab 2: Regular Expression to NFA (Thompson Construction)
# Fully Fixed Version (Supports Infix Expressions)
# =========================================================

state_count = 0


def new_state():
    global state_count
    state = f"q{state_count}"
    state_count += 1
    return state


class NFA:
    def __init__(self, start, accept, transitions):
        self.start = start
        self.accept = accept
        self.transitions = transitions


# ---------- Infix to Postfix Conversion ----------
def precedence(op):
    if op == '*':
        return 3
    elif op == '.':
        return 2
    elif op == '|':
        return 1
    return 0


def infix_to_postfix(regex):
    stack = []
    postfix = ""

    for char in regex:
        if char.isalnum():
            postfix += char
        elif char == '(':
            stack.append(char)
        elif char == ')':
            while stack and stack[-1] != '(':
                postfix += stack.pop()
            stack.pop()
        else:
            while stack and precedence(stack[-1]) >= precedence(char):
                postfix += stack.pop()
            stack.append(char)

    while stack:
        postfix += stack.pop()

    return postfix


# ---------- Thompson Construction ----------
def basic_nfa(symbol):
    start = new_state()
    end = new_state()
    transitions = {(start, symbol): [end]}
    return NFA(start, end, transitions)


def concat(nfa1, nfa2):
    transitions = {**nfa1.transitions, **nfa2.transitions}
    transitions[(nfa1.accept, 'ε')] = [nfa2.start]
    return NFA(nfa1.start, nfa2.accept, transitions)


def union(nfa1, nfa2):
    start = new_state()
    end = new_state()
    transitions = {**nfa1.transitions, **nfa2.transitions}

    transitions[(start, 'ε')] = [nfa1.start, nfa2.start]
    transitions[(nfa1.accept, 'ε')] = [end]
    transitions[(nfa2.accept, 'ε')] = [end]

    return NFA(start, end, transitions)


def kleene(nfa):
    start = new_state()
    end = new_state()
    transitions = dict(nfa.transitions)

    transitions[(start, 'ε')] = [nfa.start, end]
    transitions[(nfa.accept, 'ε')] = [nfa.start, end]

    return NFA(start, end, transitions)


def postfix_to_nfa(postfix):
    stack = []

    for char in postfix:
        if char.isalnum():
            stack.append(basic_nfa(char))

        elif char == '*':
            nfa = stack.pop()
            stack.append(kleene(nfa))

        elif char == '.':
            nfa2 = stack.pop()
            nfa1 = stack.pop()
            stack.append(concat(nfa1, nfa2))

        elif char == '|':
            nfa2 = stack.pop()
            nfa1 = stack.pop()
            stack.append(union(nfa1, nfa2))

    return stack.pop()


def display_nfa(nfa):
    print("\n===== NFA Transition Table =====")
    print("Start State :", nfa.start)
    print("Accept State:", nfa.accept)
    print("\nTransitions:")
    for (state, symbol), next_states in nfa.transitions.items():
        for ns in next_states:
            print(f"{state} -- {symbol} --> {ns}")


# ---------- Main Function ----------
def main():
    global state_count
    state_count = 0

    print("Compiler Design Lab - Lab 2")
    print("Regular Expression to NFA (Thompson Construction)\n")

    print("Instructions:")
    print("Use '.' for concatenation")
    print("Use '|' for union")
    print("Use '*' for Kleene star")
    print("Brackets supported: ( )")
    print("\nValid Inputs:")
    print("a|b")
    print("a.b")
    print("a*")
    print("(a|b).c\n")

    regex = input("Enter Regular Expression: ")

    try:
        postfix = infix_to_postfix(regex)
        print("\nPostfix Expression:", postfix)

        nfa = postfix_to_nfa(postfix)
        display_nfa(nfa)

    except Exception as e:
        print("Error:", e)
        print("Check your regex format.")


if __name__ == "__main__":
    main()
