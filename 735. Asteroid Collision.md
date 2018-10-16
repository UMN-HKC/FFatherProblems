## Solution1
``` java
class Solution {
    public int[] asteroidCollision(int[] asteroids) {
        Stack<Integer> stack = new Stack<>();
        for (int asteroid : asteroids) {
            if (asteroid > 0) {
                stack.push(asteroid);
            }
            else {
                while (!stack.empty() && stack.peek() > 0 && stack.peek() < -asteroid) {
                    stack.pop();
                }
                if (!stack.empty() && stack.peek() == -asteroid) {
                    stack.pop();
                }
                else if (stack.empty() || stack.peek() < 0){
                    stack.push(asteroid);
                }
            }
        }
        return toArray(stack);
    }
    private int[] toArray(Stack<Integer> stack) {
        int size = stack.size();
        int i = 0; 
        int[] result = new int[size]; 
        for (int num : stack) {
            result[i++] = num;
        }
        return result;
    }
}
```

## note
* natural to think of using stack to solve this problem, because we will want to pop the most recent asteroid 
and see if collide with the upcoming asteroid.
* time O(n), space O(n)
