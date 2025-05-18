# Analyze-and-Visualize-DNA-k-mer-Frequency
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

# Input DNA sequence
dna_seq = "gcgctcggcaggataacgtcaccctaaaacgtaacgttgtgcgatgacgaccggcgctcg"
freq = {}

# Get k value (must be >= 3)
k = int(input("Enter k (>= 3): "))
while k < 3:
    k = int(input("Please enter a value of k >= 3: "))

seq_len = len(dna_seq)

# Step 1: Count k-mer frequencies using a dictionary
for i in range(seq_len - k + 1):
    kmer = dna_seq[i:i+k]
    freq[kmer] = freq.get(kmer, 0) + 1

# Step 2: Find the most frequent k-mer
top_kmer = max(freq, key=freq.get)
print(f"Most frequent {k}-mer: '{top_kmer}' (count: {freq[top_kmer]})")

# Step 3: Slide a window across the sequence
window_size = 30
step_size = 5
densities = []

for start in range(0, seq_len - window_size + 1, step_size):
    window = dna_seq[start:start + window_size]
    count = 0
    for i in range(len(window) - k + 1):
        if window[i:i+k] == top_kmer:
            count += 1
    densities.append(count)

# Step 4: Convert to 2D array for heatmap
density_matrix = np.array(densities).reshape(1, -1)

# Step 5: Plot the heatmap
plt.figure(figsize=(12, 2))
sns.heatmap(density_matrix, cmap='Reds', cbar_kws={'label': f'{top_kmer} frequency'})
plt.xlabel("Sequence Position (by window)")
plt.yticks([])
plt.title(f"Heatmap of '{top_kmer}' (most frequent {k}-mer) Density")
plt.tight_layout()
plt.show()
