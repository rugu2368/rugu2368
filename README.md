# File path
file_path = "C:/path/to/sequences.txt"

# Function to read sequences from a file
def read_sequences(file_path):
    with open(file_path, 'r') as file:
        lines = file.readlines()
        reference_seq = lines[0].strip()  # First line as reference sequence
        sample_seq = lines[1].strip()     # Second line as sample sequence
    return reference_seq, sample_seq

# Load sequences from the file
reference_seq, sample_seq = read_sequences(file_path)

# Display loaded sequences
print("Reference Sequence:", reference_seq)
print("Sample Sequence:", sample_seq)
           [or]
# Sample DNA sequences for comparison
reference_seq = "ATGCGTACGTAGCT"
sample_seq = "ATGCGTTCGTAGAT"

# Function to identify mutations
def find_mutations(ref, sample):
    mutations = []
    min_len = min(len(ref), len(sample))

    for i in range(min_len):
        if ref[i] != sample[i]:  # Detect mismatch (substitution)
            mutations.append((i, ref[i], sample[i]))

    if len(ref) > len(sample):  # Detect deletions
        for i in range(min_len, len(ref)):
            mutations.append((i, ref[i], "-"))
    elif len(ref) < len(sample):  # Detect insertions
        for i in range(min_len, len(sample)):
            mutations.append((i, "-", sample[i]))

    return mutations

# Find and display mutations
mutations = find_mutations(reference_seq, sample_seq)
print("Mutations found (position, ref_base, sample_base):", mutations)

