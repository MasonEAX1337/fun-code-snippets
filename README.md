# Fun Code Snippets 🚀

This repository is a collection of small but fun coding experiments and ideas. Each snippet has a description of the thought process or inspiration behind it.  

## Snippets Included
1. **Gravity Drop Calculator**
   - **Description:** While learning about Newton's Law of Universal Gravitation in physics class, I wondered how far you'd have to move away from Earth for gravity to drop from 9.81 m/s² to 9.80 m/s². I visualized the code to calculate this in my head during class and then coded it when I got home.  
   - **Language:** C++
   - **Purpose:** To calculate the distance at which gravity drops slightly.

---

### Snippet 1: Gravity Drop Calculator (C++)  
Here’s the script along with its explanation:

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
} ```

#### Result
Interestingly, the result was approximetly 4 miles, while the highest altitude on Earth, which is the summit of Mount Everest, is approximately 5.5 miles high.

