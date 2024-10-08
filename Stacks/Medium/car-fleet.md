# Car Fleet

[https://leetcode.com/problems/car-fleet/](https://leetcode.com/problems/car-fleet/)

### **Problem**

How many cars will arrive together (as a fleet) at a destination given that each car drives at its own speed and that cars that catch up to others will travel at the speed of the slowest car.

- given an integer **target** representing the target position
- **position[] -** position of the $i$th car
- **speed[] -** speed of the $i$th car

All cars are driving toward the target. A car fleet is a group of cars that arrive at the destination at the same time, either because they are driving at the same speed or because faster cars slow down when they catch up to slower cars. If a car catches up to another car, it forms a fleet with that car, and they travel together at the speed of the slower car.

### Solution

Start with thinking of how we can represent the speeds/positions of these cars as a system of linear equations. If we consider the $time$ it will take for the cars to reach the destination position, we can simply conclude any car’s linear function that intersect with another will be considered a fleet.

Recall: $time=\frac{target-position[i]}{speed[i]}$

The intuition is to calculate the time it will take each car to reach the target, but we do this by processing cars closest to the destination to the farthest, meaning we must sort the positions in descending order. 

- if the car closest to the target destination will reach in $t = 2$ seconds and the car BEHIND it will reach in $t = 1.5$ seconds, the car behind it will reach the first car and must slow down as a result
- we can simply count the number of cars that have a slower time to reach the destination
    - note you can also complete this problem with a stack, however, it is more inefficient and way less intuitive than this counter method.
    - add the cars to the stack and compare them, pop the one on the top of the stack if the the car added before takes more time than the second.

```python
class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        # sort the position array in descending order (maintaining the speed order)
        combined = [(pos, spd) for pos, spd in zip(position, speed)]
        sorted_combined = sorted(combined, key=lambda x: x[0], reverse=True)

        # calculate time for each
        count, prev_time = 0, 0
        for pos, spd in sorted_combined:
            t = (target - pos) / spd

            if t > prev_time:
                count += 1
                prev_time = t
    
        return count
```