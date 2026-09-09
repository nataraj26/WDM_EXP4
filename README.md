### EX4 Implementation of Cluster and Visitor Segmentation for Navigation patterns
### DATE: 04/08/26
---
### Name: NATARAJ KUMARAN S
### Register No: 212223230137
---
### AIM: To implement Cluster and Visitor Segmentation for Navigation patterns in Python.
### Description:
<div align= "justify">Cluster visitor segmentation refers to the process of grouping or categorizing visitors to a website, 
  application, or physical location into distinct clusters or segments based on various characteristics or behaviors they exhibit. 
  This segmentation allows businesses or organizations to better understand their audience and tailor their strategies, marketing efforts, 
  or services to meet the specific needs and preferences of each cluster.</div>
  
### Procedure:
1) Read the CSV file: Use pd.read_csv to load the CSV file into a pandas DataFrame.
2) Define Age Groups by creating a dictionary containing age group conditions using Boolean conditions.
3) Segment Visitors by iterating through the dictionary and filter the visitors into respective age groups.
4) Visualize the result using matplotlib.
  
### Program:
``` python

centroids = X[:k]

# Iteration loop for K-Means convergence
for _ in range(100):  # Maximum iterations to ensure convergence

    clusters = [[] for _ in range(k)]
    cluster_indices = [[] for _ in range(k)]
    
    for idx, x in enumerate(X):
        # Find the index of the closest centroid
        distances = [abs(x - c) for c in centroids]
        closest_centroid_idx = distances.index(min(distances))
        clusters[closest_centroid_idx].append(x)
        cluster_indices[closest_centroid_idx].append(idx)

    new_centroids = []
    for i in range(k):
        if clusters[i]:
            new_centroids.append(sum(clusters[i]) / len(clusters[i]))
        else:
        # Keep old centroid if a cluster becomes empty
            new_centroids.append(centroids[i])
            
    # Check for convergence (if centroids stop changing)
    if new_centroids == centroids:
        break
    centroids = new_centroids

# Assign final labels to the dataframe for visualization/output
df["Cluster"] = 0
for i, indices in enumerate(cluster_indices):
    for idx in indices:
        df.loc[idx, "Cluster"] = i

print("Cluster-wise Output:")
for i in range(k):
    print(f"Cluster {i} (Centroid: {centroids[i]:.2f}):")
    print(clusters[i])
    print("-" * 40)

```
### Output:

<img width="590" height="221" alt="Screenshot 2026-08-04 110032" src="https://github.com/user-attachments/assets/47c38599-06b4-4d0d-b102-c3b271a3d799" />

### Visualization:
```
colors = ['red', 'green', 'blue']
plt.figure(figsize=(10, 6))

for i in range(k):
    cluster_data = [X[idx] for idx in cluster_indices[i]]
    y_vals = [i] * len(cluster_data)
    
    # Plot the scatter points
    plt.scatter(cluster_data, y_vals, color=colors[i], label=f'Cluster {i}', s=100)
    
    # Display the age value near each plotted point
    for x, y in zip(cluster_data, y_vals):
        plt.text(x, y + 0.08, str(x), fontsize=9, ha='center', va='bottom', fontweight='bold', color=colors[i])

# Plot final centroids
plt.scatter(centroids, range(k), color='black', marker='X', s=200, label='Centroids', zorder=5)
for i, c in enumerate(centroids):
    plt.text(c, i - 0.15, f"C{i}: {c:.1f}", fontsize=10, ha='center', va='top', fontweight='bold', color='black')

plt.xlabel("Age")
plt.ylabel("Cluster ID")
plt.title("Visitor Segmentation using K-Means (with Age Values)")
plt.yticks(range(k))
plt.legend()
plt.grid(True, axis='x', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.show()
```
### Output:

<img width="529" height="317" alt="Screenshot 2026-08-04 111526" src="https://github.com/user-attachments/assets/34ca31ab-f11d-42b3-bde2-eed8f4b2ce57" />

### Result:
Thus, Cluster and Visitor Segmentation for Navigation Patterns was successfully implemented in Python, and the visitor distribution across different age groups was visualized successfully using a bar chart.
