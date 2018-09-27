## Solution1
``` java
class Solution {
    public List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        List<List<Integer>> result = new LinkedList<>();
        if (graph == null || graph.length == 0 || graph[0].length == 0) {
            return result;
        }
        List<Integer> path = new LinkedList<>();
        allPathsSourceTarget(result, path, graph, 0, graph.length - 1);
        return result;
    }
    private void allPathsSourceTarget(List<List<Integer>> result, List<Integer> path, 
        int[][] graph, int source, int target) {
        
        path.add(source);
        if (source == target) {
            result.add(new LinkedList<Integer>(path));
        }
        else {
            for (int next : graph[source]) {
                allPathsSourceTarget(result, path, graph, next, target);    
            }
            
        }
        path.remove(path.size() - 1);
    }
}
```
## notes:
* dfs because need to print all possible paths. 
* need to remove the last added integer in the path because of backtracking
* pass target as graph.length - 1.
