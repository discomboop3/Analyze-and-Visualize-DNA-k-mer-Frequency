# Analyze-and-Visualize-DNA-k-mer-Frequency
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
#Randomly generated DNA Sequence
dna_seq = "gcgctcggcaggataacgtcaccctaaaacgtaacgttgtgcgatgacgaccggcgctcg"
freq = {}

k = 4
#k = int(input("Enter k (>= 3): "))
#while k < 3:
    #k = int(input("Please enter a value of k >= 3: "))

seq_len = len(dna_seq)

for i  in range (0, seq_len - 1):
    for j in range (0, seq_len):
        if (len(dna_seq[i:j]) >= k):
            if (dna_seq[i:j] in freq):
                freq[dna_seq[i:j]] += 1
            else:
                freq[dna_seq[i:j]] = 1
print(freq)
data = pd.DataFrame.from_dict(freq, orient='index')
plt.imshow(data)

plt.title( "2-D Heat Map" )
plt.show()
