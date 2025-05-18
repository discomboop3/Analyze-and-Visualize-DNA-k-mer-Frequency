import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

dna_seq = "gcgctcggcaggataacgtcaccctaaaacgtaacgttgtgcgatgacgaccggcgctcg"
freq = {}

k = 4
#k = int(input("Enter k (>= 3): "))
#while k < 3:
#    k = int(input("Please enter a value of k >= 3: "))

seq_len = len(dna_seq)


for i in range(seq_len - k + 1):
    kmer = dna_seq[i:i+k]
    freq[kmer] = freq.get(kmer, 0) + 1

top_kmer = max(freq, key=freq.get)
print(f"Most frequent {k}-mer: '{top_kmer}' (count: {freq[top_kmer]})")

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

density_matrix = np.array(densities).reshape(1, -1)

plt.figure(figsize=(12, 2))
sns.heatmap(density_matrix, cmap='Reds', cbar_kws={'label': f'{top_kmer} frequency'})
plt.xlabel("Sequence Position (by window)")
plt.yticks([])
plt.title(f"Heatmap of '{top_kmer}' (most frequent {k}-mer) Density")
plt.tight_layout()
plt.show()
![heatmap](https://github.com/user-attachments/assets/5d99a5ea-fc62-4125-9b09-714fc366d2f4)
