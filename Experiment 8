# Compiler Design Lab - Lab 8
# Program to Compute LEADING and TRAILING of a Grammar

from collections import defaultdict

# Function to compute LEADING
def compute_leading(grammar):
    leading = defaultdict(set)
    changed = True

    while changed:
        changed = False
        for lhs in grammar:
            for production in grammar[lhs]:
                if len(production) == 0:
                    continue

                first = production[0]

                # Case 1: First symbol is terminal
                if not first.isupper():
                    if first not in leading[lhs]:
                        leading[lhs].add(first)
                        changed = True

                # Case 2: First symbol is non-terminal
                else:
                    for symbol in leading[first]:
                        if symbol not in leading[lhs]:
                            leading[lhs].add(symbol)
                            changed = True

                # Case 3: Handle patterns like A->Ba
                if len(production) > 1 and production[0].isupper():
                    second = production[1]
                    if not second.isupper():
                        if second not in leading[lhs]:
                            leading[lhs].add(second)
                            changed = True

    return leading


# Function to compute TRAILING
def compute_trailing(grammar):
    trailing = defaultdict(set)
    changed = True

    while changed:
        changed = False
        for lhs in grammar:
            for production in grammar[lhs]:
                if len(production) == 0:
                    continue

                last = production[-1]

                # Case 1: Last symbol is terminal
                if not last.isupper():
                    if last not in trailing[lhs]:
                        trailing[lhs].add(last)
                        changed = True

                # Case 2: Last symbol is non-terminal
                else:
                    for symbol in trailing[last]:
                        if symbol not in trailing[lhs]:
                            trailing[lhs].add(symbol)
                            changed = True

                # Case 3: Handle patterns like A->aB
                if len(production) > 1 and production[-1].isupper():
                    second_last = production[-2]
                    if not second_last.isupper():
                        if second_last not in trailing[lhs]:
                            trailing[lhs].add(second_last)
                            changed = True

    return trailing


# Main Program
def main():
    grammar = {}

    try:
        n = int(input("Enter number of productions: "))
        print("Enter productions in format A->aB|b (No spaces):")

        count = 0
        while count < n:
            prod = input().strip()

            if "->" not in prod:
                print("Invalid format! Use A->aB|b")
                continue

            lhs, rhs = prod.split("->")
            productions = rhs.split("|")
            grammar[lhs] = productions
            count += 1

        leading = compute_leading(grammar)
        trailing = compute_trailing(grammar)

        print("\nLEADING Sets:")
        for non_terminal in grammar:
            print(f"LEADING({non_terminal}) = {{ {', '.join(sorted(leading[non_terminal]))} }}")

        print("\nTRAILING Sets:")
        for non_terminal in grammar:
            print(f"TRAILING({non_terminal}) = {{ {', '.join(sorted(trailing[non_terminal]))} }}")

    except ValueError:
        print("Error: Please enter a valid number.")
    except Exception as e:
        print("Unexpected Error:", e)


if __name__ == "__main__":
    main()
