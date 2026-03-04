# Lab 7: Shift Reduce Parser (Error Fixed & Robust Version)

def shift_reduce_parser(grammar, start_symbol, input_string):
    stack = ""
    input_buffer = input_string + "$"
    step = 1

    print("\nStep\tStack\t\tInput Buffer\tAction")

    while True:
        reduced = False

        # Try Reduction
        for lhs in grammar:
            for rhs in grammar[lhs]:
                if rhs != "" and stack.endswith(rhs):
                    print(f"{step}\t{stack}\t\t{input_buffer}\t\tReduce {lhs}->{rhs}")
                    stack = stack[:-len(rhs)] + lhs
                    step += 1
                    reduced = True
                    break
            if reduced:
                break

        if reduced:
            continue

        # Shift Operation
        if len(input_buffer) > 0:
            print(f"{step}\t{stack}\t\t{input_buffer}\t\tShift")
            stack += input_buffer[0]
            input_buffer = input_buffer[1:]
            step += 1
        else:
            break

        # Accept Condition
        if stack == start_symbol and input_buffer == "$":
            print(f"{step}\t{stack}\t\t{input_buffer}\t\tAccept")
            return True

        # Reject Condition
        if input_buffer == "$" and stack != start_symbol:
            print(f"{step}\t{stack}\t\t{input_buffer}\t\tReject")
            return False


# Main Program (Safe Input Handling)
grammar = {}

try:
    n = int(input("Enter number of productions: "))
    print("Enter productions in format A->aB|b (No spaces):")

    count = 0
    while count < n:
        prod = input().strip()

        # Skip empty lines (THIS FIXES YOUR ERROR)
        if prod == "":
            print("Empty input! Please enter a valid production like E->E+E|i")
            continue

        if "->" not in prod:
            print("Invalid format! Use A->aB|b")
            continue

        lhs, rhs = prod.split("->")
        grammar[lhs] = rhs.split("|")
        count += 1

    start_symbol = input("Enter start symbol: ").strip()
    input_string = input("Enter input string: ").strip()

    result = shift_reduce_parser(grammar, start_symbol, input_string)

    if result:
        print("\nString Accepted by Shift Reduce Parser.")
    else:
        print("\nString Rejected by Shift Reduce Parser.")

except Exception as e:
    print("Error:", e)
