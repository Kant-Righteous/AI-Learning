# AI-Learning

这是一个关于人工智能学习的个人代码仓库，包含教程（Tutorials）和练习（Exercises），涵盖搜索算法、约束满足问题等核心 AI 主题。

## 目录结构

### 📂 TP (Travaux Pratiques / Practical Works)
核心学习材料，分为教程和练习。

- **`Tutorial/`**: Jupyter Notebook 格式的基础教程。
  - Python 基础 (列表, 字典, Numpy, Pandas)
  - 数据处理 (Pandas)
  - 面向对象编程 (OOP)

- **`Exercise/TP/`**: 核心算法的练习与实现代码。
  - **`TP1/` (无信息搜索)**: `Taquin` (推盘游戏) 的 BFS 和 DFS 实现。
  - **`TP2/` (有信息搜索)**: `Taquin` 的 A* 算法及启发式函数实现。
  - **`TP3/` (SAT & CSP)**: Sudoku (数独) 问题的 SAT 求解 (CNF 转化)。

### 📂 Data
存放项目或练习所需的数据集文件。

## 算法详解 (Algorithm Details)

本项目重点实现了经典的搜索算法，并应用于解决 Taquin (推盘游戏) 和 Sudoku (数独) 问题。

### 1. 搜索算法对比 (Search Algorithms Comparison)

下表总结了无信息搜索 (BFS, DFS) 和有信息搜索 (A*) 的主要区别：

| 算法 | 时间复杂度 | 空间复杂度 | 完备性 | 最优性 | 特点 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **BFS**<br>(广度优先) | $O(b^d)$ | $O(b^d)$ | ✅ 是 | ✅ 是$^1$ | 找最短路径，但在深层解时**内存消耗极大**。 |
| **DFS**<br>(深度优先) | $O(b^m)$ | $O(b \cdot m)$ | ❌ 否 | ❌ 否 | **内存效率高**，但可能陷入死循环或找不到解。 |
| **A\***<br>(启发式) | 指数级 | 指数级 | ✅ 是 | ✅ 是$^2$ | 结合了 BFS 的完备性和贪婪算法的效率，依赖 $h(n)$。 |

> **注**:
> *   $b$: 分支因子 (branching factor), $d$: 最浅解深度 (depth), $m$: 最大搜索深度。
> *   $^1$: 前提是每步代价相等 (step cost = 1)。
> *   $^2$: 前提是启发式函数 $h(n)$ 是 **可采纳的 (admissible)**。

### 2. 无信息搜索 (Uninformed Search) - TP1
在 `TP/Exercise/TP/TP1` 中，我们通过推盘游戏比较了 BFS 和 DFS。
- **广度优先搜索 (BFS)**: 逐层扩展节点。能够保证找到从初始状态到目标状态的最短路径（最少移动步数），但随着步数增加，需要存储的节点数量呈指数级增长，容易耗尽内存。
- **深度优先搜索 (DFS)**: 尽可能深地搜索树的分支。由于推盘游戏的状态空间可能有环或极深，直接应用标准 DFS 可能会导致无限循环或在错误路径上搜索过久。

### 3. 有信息搜索 (Informed Search) - TP2
在 `TP/Exercise/TP/TP2` 中，我们引入了 **A\*** 算法。
- **启发式函数 (Heuristic Function, $h(n)$)**: A* 利用 $h(n)$ 来估计从当前节点到目标节点的代价。
- **实现细节**:
    - 使用 **曼哈顿距离 (Manhattan Distance)** 或 **错位瓦片数 (Misplaced Tiles)** 作为 $h(n)$。
    - $f(n) = g(n) + h(n)$，其中 $g(n)$ 是从起点到当前节点的实际代价。
    - 相比 BFS，A* 能够大幅减少需要扩展的节点数量，从而更快地找到最优解。

### 4. 约束满足问题 (CSP & SAT) - TP3
在 `TP/Exercise/TP/TP3` 中，我们将 **Sudoku (数独)** 问题建模为 SAT 问题。
- **SAT (布尔可满足性问题)**: 判断是否存在一组布尔变量的赋值，使得给定的逻辑公式为真。
- **建模方法**:
    - 使用 **CNF (合取范式)** 来描述数独规则（如“每行每列每宫必须包含 1-9”）。
    - 变量 $X_{i,j,k}$ 表示第 $i$ 行第 $j$ 列填入数字 $k$。
- **求解**: 使用 `python-sat` 库的求解器快速找到满足所有约束的填法。

## 环境
- Python 3.x
- Jupyter Notebook
- 依赖库: `numpy`, `pandas`, `python-sat` (用于 TP3)
