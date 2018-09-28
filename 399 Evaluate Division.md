## Solution1

``` java
class Solution {
    public double[] calcEquation(String[][] equations, double[] values, String[][] queries) {
        
        Map<String, Integer> vertices = findVertices(equations);
        double[][] graph = buildGraph(equations, values, vertices);
        double[] result = new double[queries.length];
        boolean[] visited = new boolean[vertices.size()];
        
        for (int i = 0; i < queries.length; i++) {
            String from = queries[i][0];
            String to = queries[i][1];
            if (!vertices.containsKey(from) || !vertices.containsKey(to) ){
                result[i] = -1;
            }
            else {
                Arrays.fill(visited, false);    
                result[i] = dfs(vertices.get(from), vertices.get(to), graph, visited);
            }
        }
        return result;
    }
    private Map<String, Integer> findVertices(String[][] equations) {
        Map<String, Integer> vertices = new HashMap<>();
        for (String[] equation : equations) {
            if (!vertices.containsKey(equation[0])) {
                vertices.put(equation[0], vertices.size());
            }
            if (!vertices.containsKey(equation[1])) {
                vertices.put(equation[1], vertices.size());
            }
        }
        return vertices;
    }
    private double[][] buildGraph(String[][] equations, double[] values, Map<String, Integer> vertices) {
        double[][] graph = new double[vertices.size()][vertices.size()];
        for (int i = 0; i < graph.length; i++) {
            graph[i][i] = 1;
        }
        for (int j = 0; j < equations.length; j++) {
            int x = vertices.get(equations[j][0]);
            int y = vertices.get(equations[j][1]);
            graph[x][y] = values[j];
            graph[y][x] = 1 / values[j];
        }
        return graph;
    }
    private double dfs(int from, int to, double[][] graph, boolean[] visited) {
        for (int i = 0; i < graph[from].length; i++) {
            if (graph[from][i] != 0 && !visited[i]) {
                if (i != to) {
                    visited[i] = true;
                    double result = dfs(i, to, graph, visited);
                    if (result != -1) {
                        return graph[from][i] * result;
                    }
                    visited[i] = false;
                }
                else {
                    return graph[from][i];
                }      
            }
        }
     return -1;   
    }
}
```

## Notes
* need to conceptualize this problem into a graph problem
* solve it in an adjacency matrix. first find all vertices, since "a", "b", "c" ... 
cannot represent index, so we need a hashmap to store the vertices. After finding all 
vertices, we build the graph and do depth first search.
* need to set back the boolean value before each query execution and after each dfs.
