# 2021l_INT3401_8_Pacman
Solutions to Pacman project assignment.

4 câu hỏi đầu tiên yêu cầu cài đặt các thuật toán tìm kiếm DFS, BFS, UCS và A* search. Về mặt ý tưởng thì 4 thuật toán này là tương tự. Chỉ khác duy nhất ở cấu trúc dữ liệu dùng để lưu trữ đường đi của pacman. Đối với DFS và BFS thì cấu trúc mình chọn là Stack và Queue. Đối với UCS và A* thì đều sử dụng Priority Queue với cost là tham số mức độ ưu tiên. Ở A* thì chi phí còn phải cộng thêm với giá trị heuristic. Mình sẽ viết thêm một hàm search để có thể dùng chung với 4 bài toán trên với tham số chỉ thay đổi ở giá trị "fringe":
  def graphSearch(fringe, problem):
    fringe.push([(problem.getStartState(), "Stop", 0)])
    visited = []
    while not fringe.isEmpty():
        path = fringe.pop()
        curr_state = path[-1][0]
        if problem.isGoalState(curr_state):
            return [x[1] for x in path][1:]
        if curr_state not in visited:
            visited.append(curr_state)
            for successor in problem.getSuccessors(curr_state):
                if successor[0] not in visited:
                    successorPath = list(path)
                    successorPath.append(successor)
                    fringe.push(successorPath)
