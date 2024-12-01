# Fun Code Snippets 🚀

This repository is a collection of small but fun coding experiments and ideas. Each snippet has a description of the thought process or inspiration behind it.  

## Snippets Included
1. **Gravity Drop Calculator**
   - **Description:** While learning about Newton's Law of Universal Gravitation in physics class, I wondered how far you'd have to move away from Earth for gravity to drop from 9.81 m/s² to 9.80 m/s². I visualized the code to calculate this in my head during class and then coded it when I got home.  
   - **Language:** C++
   - **Purpose:** To calculate the distance at which gravity drops slightly.

2. **Consecutive Heads Simulator**
   - **Description:** This program simulates flipping a coin until a desired number of consecutive heads is achieved. I was curious the difference of attempts it took to get 2 vs. 3 consecutive heads in a row in a coin flip, then wanted to see the results at scale. Although I strongly prefer C-based syntax languages, I knew python would make it ridiculously easy to create and render a graph due to the vast simplistic libraries python has to offer. 
   - **Language:** Python  
   - **Purpose:** To calculate the average number of flips required to get a specific number of consecutive heads.

### Snippet 1: Gravity Drop Calculator (C++)  

#### **Code:**

```cpp
double getAltitudeForGravity(float targetGravity) {
    // Formula: r = sqrt((G * m1) / g)
    const double gravitation = 6.67430e-11; // Gravitational constant (m³/kg/s²)
    const double mass = 5.972e24;          // Mass of Earth (kg)
    const double earthRadius = 6371000;    // Radius of Earth at sea level (meters)

    // Total distance from Earth's center
    double totalDistance = std::sqrt((gravitation * mass) / targetGravity);

    // Altitude above Earth's surface
    double altitude = totalDistance - earthRadius;

    // Convert altitude to miles
    return altitude / 1609.34;
} 
```

#### Explanation
Newton's Law of Universal Gravitation:
![Equation](https://latex.codecogs.com/png.latex?g%20%3D%20%5Cfrac%7BG%20%5Ccdot%20M%7D%7Br%5E2%7D)
Where:
- G: Gravitational constant.
- M: Mass of Earth.
- r: Distance from Earth's center.
The formula is rearranged to compute r, and Earth's radius is subtracted to get the altitude above the surface.

#### Result
Interestingly, the result was approximetly 4 miles, while the highest altitude on Earth, which is the summit of Mount Everest, is approximately 5.5 miles high.

### Snippet 2: Consecutive Heads Simulator (Python)  

#### **Code:**
```python
import matplotlib.pyplot as plt
import secrets
import math

# Initialize data storage
x = []  # Number of consecutive heads required
y = []  # Average number of tries to achieve consecutive heads

# Parameters for the simulation
num_trials = 100  # Number of trials per consecutive head count
num_max = 10  # Maximum number of consecutive heads to simulate

# Simulate for each count of consecutive heads (1 to num_max)
for i in range(1, num_max + 1):
    y_trials = []  # Store the number of tries for each trial
    for _ in range(num_trials):
        num_heads = 0  # Total heads flipped
        num_tails = 0  # Total tails flipped
        last_flip = -1  # Last flip result (-1 indicates no flip yet)
        consecutive_heads = 0  # Current streak of consecutive heads

        # Keep flipping until the desired consecutive heads are achieved
        while consecutive_heads != i:
            if secrets.choice([0, 1]) == 0:  # Flip results in tails
                num_tails += 1
                consecutive_heads = 0  # Reset streak
                last_flip = 0
            else:  # Flip results in heads
                num_heads += 1
                if last_flip == 1:  # Increment streak if the last flip was heads
                    consecutive_heads += 1
                else:  # Reset streak if this is the first head in a row
                    consecutive_heads = 1
                last_flip = 1
        
        # Total number of flips (heads + tails) for this trial
        y_trials.append(num_tails + num_heads)

    # Calculate the average number of tries for this consecutive head count
    average = math.floor(sum(y_trials) / len(y_trials))
    x.append(i)  # Store the consecutive head count
    y.append(average)  # Store the average number of tries

# Output the average number of tries for each consecutive head count
print(y)

# Plot the results
plt.plot(x, y, label='Average Tries per Consecutive Heads', color='blue', linestyle='--', marker='o')

# Add labels, title, and legend
plt.xlabel('Number of Consecutive Heads')
plt.ylabel('Average Number of Coin Flips')
plt.title('Simulating Flips: Tries to Achieve Consecutive Heads')
plt.legend()

# Display the graph
plt.show()
```

---

#### Explanation
This program simulates flipping a coin until a specific number of consecutive heads is achieved. For example:
- If `i = 1`, it calculates the average number of flips required to get one head.
- If `i = 10`, it calculates the average number of flips required to get 10 consecutive heads.

The number of flips required increases exponentially with the number of consecutive heads due to the decreasing probability of getting `i` consecutive heads:
P(consecutive heads) = (0.5)^i

Additionally, like any good scientist, I made sure to average the results. In my physics class, every time we do a lab, no one enjoys running multiple trials to gather accurate data—it’s often seen as tedious. However, with the limitless capabilities of computers, I decided to take it to the next level by running 100 trials automatically. Projects like this always spark my interest in computer science because they remind me that when I have a computer, almost anything is possible.

#### Result
The program plots a graph showing the relationship between the number of consecutive heads and the average number of flips required. Below is an example graph generated by the program:
![image](https://github.com/user-attachments/assets/b87e5d5b-0fc3-4720-b343-a6454af43ce3)


