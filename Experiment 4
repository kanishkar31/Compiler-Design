"""
Compiler Design Lab - Lab 4
Program: Removal of Left Recursion and Left Factoring
Description:
This program removes immediate left recursion and performs left factoring
for a given context-free grammar production.
"""

def remove_left_recursion(production):
    # Example input: A->Aa|b
    left, right = production.split("->")
    rules = right.split("|")

    alpha = []  # left recursive part
    beta = []   # non-left recursive part

    for rule in rules:
        if rule.startswith(left):
            alpha.append(rule[len(left):])
        else:
            beta.append(rule)

    if not alpha:
        print("\nNo Left Recursion Detected.")
        print("Production remains:", production)
        return

    print("\nAfter Removing Left Recursion:")
    new_left = left + "'"

    # A -> βA'
    new_rules_1 = [b + new_left for b in beta]
    print(f"{left} -> {' | '.join(new_rules_1)}")

    # A' -> αA' | ε
    new_rules_2 = [a + new_left for a in alpha]
    new_rules_2.append("ε")
    print(f"{new_left} -> {' | '.join(new_rules_2)}")


def left_factoring(production):
    # Example input: A->ab|ac
    left, right = production.split("->")
    rules = right.split("|")

    prefix = rules[0]

    for rule in rules[1:]:
        i = 0
        while i < min(len(prefix), len(rule)) and prefix[i] == rule[i]:
            i += 1
        prefix = prefix[:i]

    if prefix == "":
        print("\nNo Left Factoring Needed.")
        print("Production remains:", production)
        return

    print("\nAfter Left Factoring:")
    new_left = left + "'"

    print(f"{left} -> {prefix}{new_left}")

    new_rules = []
    for rule in rules:
        if rule.startswith(prefix):
            suffix = rule[len(prefix):]
            if suffix == "":
                suffix = "ε"
            new_rules.append(suffix)

    print(f"{new_left} -> {' | '.join(new_rules)}")


def main():
    print("===================================")
    print(" Compiler Design Lab - Lab 4")
    print(" Left Recursion & Left Factoring")
    print("===================================")
    print("\nInput format example:")
    print("A->Aa|b  (Left Recursion)")
    print("A->ab|ac (Left Factoring)")

    production = input("\nEnter Production: ").strip()

    if "->" not in production:
        print("Invalid Production Format! Use A->Aa|b format.")
        return

    print("\nOriginal Production:", production)

    # Remove Left Recursion
    remove_left_recursion(production)

    # Perform Left Factoring
    left_factoring(production)


if __name__ == "__main__":
    main()
