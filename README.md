# gold# Simple Gold Code Generator using LFSR
import numpy as np

# Function to generate an LFSR sequence
def lfsr(seed, taps, length):
    """Generate LFSR sequence."""
    state = seed
    output = []
    
    for _ in range(length):
        output.append(state[-1])  # Output the last bit
        feedback = np.bitwise_xor.reduce([state[i] for i in taps])  # XOR of the tap positions
        state = [feedback] + state[:-1]  # Shift right and add feedback at the start
    return output

# Parameters for LFSR
seed1 = [1, 0, 0, 1, 1]  # Initial seed for LFSR 1
seed2 = [1, 1, 0, 0, 1]  # Initial seed for LFSR 2
taps = [2, 4]            # Tap positions (example)

# Length of the Gold code sequence
length = 31

# Generate two LFSR sequences
lfsr1 = lfsr(seed1, taps, length)
lfsr2 = lfsr(seed2, taps, length)

# XOR the two LFSR sequences to generate a Gold Code
gold_code = [a ^ b for a, b in zip(lfsr1, lfsr2)]

# Output the Gold Code sequence
print("Gold Code Sequence:", gold_code)
