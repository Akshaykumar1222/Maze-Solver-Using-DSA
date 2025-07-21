import java.util.*;

public class MazeSolver {

    static int[][] maze = {
        {0, 1, 0, 0, 0},
        {0, 1, 0, 1, 0},
        {0, 0, 0, 1, 0},
        {1, 1, 0, 0, 0},
        {0, 0, 0, 1, 0}
    };

    static int[] dx = {0, 1, 0, -1};
    static int[] dy = {1, 0, -1, 0};
    static int n = maze.length;
    static int m = maze[0].length;

    static int[] start = {0, 0};
    static int[] end = {4, 4};

    static boolean isValid(int x, int y, boolean[][] visited) {
        return x >= 0 && y >= 0 && x < n && y < m && maze[x][y] == 0 && !visited[x][y];
    }

    // DFS
    static List<int[]> dfs() {
        Stack<List<int[]>> stack = new Stack<>();
        List<int[]> path = new ArrayList<>();
        path.add(start);
        stack.push(path);
        boolean[][] visited = new boolean[n][m];

        while (!stack.isEmpty()) {
            List<int[]> currentPath = stack.pop();
            int[] pos = currentPath.get(currentPath.size() - 1);
            int x = pos[0], y = pos[1];

            if (x == end[0] && y == end[1]) return currentPath;
            visited[x][y] = true;

            for (int i = 0; i < 4; i++) {
                int nx = x + dx[i], ny = y + dy[i];
                if (isValid(nx, ny, visited)) {
                    List<int[]> newPath = new ArrayList<>(currentPath);
                    newPath.add(new int[]{nx, ny});
                    stack.push(newPath);
                }
            }
        }
        return null;
    }

    // BFS
    static List<int[]> bfs() {
        Queue<List<int[]>> queue = new LinkedList<>();
        List<int[]> path = new ArrayList<>();
        path.add(start);
        queue.add(path);
        boolean[][] visited = new boolean[n][m];

        while (!queue.isEmpty()) {
            List<int[]> currentPath = queue.poll();
            int[] pos = currentPath.get(currentPath.size() - 1);
            int x = pos[0], y = pos[1];

            if (x == end[0] && y == end[1]) return currentPath;
            visited[x][y] = true;

            for (int i = 0; i < 4; i++) {
                int nx = x + dx[i], ny = y + dy[i];
                if (isValid(nx, ny, visited)) {
                    List<int[]> newPath = new ArrayList<>(currentPath);
                    newPath.add(new int[]{nx, ny});
                    queue.add(newPath);
                }
            }
        }
        return null;
    }

    // A* Algorithm
    static List<int[]> aStar() {
        PriorityQueue<Node> open = new PriorityQueue<>(Comparator.comparingInt(n -> n.f));
        boolean[][] visited = new boolean[n][m];
        open.add(new Node(start, 0, heuristic(start, end), new ArrayList<>()));

        while (!open.isEmpty()) {
            Node current = open.poll();
            int[] pos = current.position;
            int x = pos[0], y = pos[1];

            if (x == end[0] && y == end[1]) {
                current.path.add(pos);
                return current.path;
            }
            if (visited[x][y]) continue;
            visited[x][y] = true;

            for (int i = 0; i < 4; i++) {
                int nx = x + dx[i], ny = y + dy[i];
                if (isValid(nx, ny, visited)) {
                    List<int[]> newPath = new ArrayList<>(current.path);
                    newPath.add(pos);
                    int g = current.g + 1;
                    int h = heuristic(new int[]{nx, ny}, end);
                    open.add(new Node(new int[]{nx, ny}, g, g + h, newPath));
                }
            }
        }
        return null;
    }

    // Dijkstra's Algorithm
    static List<int[]> dijkstra() {
        PriorityQueue<Node> pq = new PriorityQueue<>(Comparator.comparingInt(n -> n.g));
        boolean[][] visited = new boolean[n][m];
        pq.add(new Node(start, 0, 0, new ArrayList<>()));

        while (!pq.isEmpty()) {
            Node current = pq.poll();
            int[] pos = current.position;
            int x = pos[0], y = pos[1];

            if (x == end[0] && y == end[1]) {
                current.path.add(pos);
                return current.path;
            }
            if (visited[x][y]) continue;
            visited[x][y] = true;

            for (int i = 0; i < 4; i++) {
                int nx = x + dx[i], ny = y + dy[i];
                if (isValid(nx, ny, visited)) {
                    List<int[]> newPath = new ArrayList<>(current.path);
                    newPath.add(pos);
                    int g = current.g + 1;
                    pq.add(new Node(new int[]{nx, ny}, g, g, newPath));
                }
            }
        }
        return null;
    }

    static int heuristic(int[] a, int[] b) {
        return Math.abs(a[0] - b[0]) + Math.abs(a[1] - b[1]);
    }

    public static void main(String[] args) {
        System.out.println("DFS Path: " + formatPath(dfs()));
        System.out.println("BFS Path: " + formatPath(bfs()));
        System.out.println("A* Path: " + formatPath(aStar()));
        System.out.println("Dijkstra Path: " + formatPath(dijkstra()));
    }

    static String formatPath(List<int[]> path) {
        if (path == null) return "No path found";
        StringBuilder sb = new StringBuilder();
        for (int[] p : path) {
            sb.append(Arrays.toString(p)).append(" ");
        }
        return sb.toString();
    }

    static class Node {
        int[] position;
        int g, f;
        List<int[]> path;

        Node(int[] position, int g, int f, List<int[]> path) {
            this.position = position;
            this.g = g;
            this.f = f;
            this.path = path;
        }
    }
}
