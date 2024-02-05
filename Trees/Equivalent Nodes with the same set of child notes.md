#Tree #BinaryTree #BitMask #HashMap


#Medium

---
Дано бинарное дерево где у каждой ноды в качестве значения выступают буквы английского алфавита `A-Z`(по одной), нужно найти пару идентичных вершин, у которых в поддереве будет одинаковое множество дочерних вершин.


****
**Intuition**
По мере прохождения по дереву DFS'ом вычисляем побитовую маску для каждой вершины и ее поддерева - `O(1)`, добавляем ее в хэшмап где в качестве ключа - битмаска, а в качестве значения массив с названиями вершин с такой же битмаской. После прохода DFS, проходимся циклом по хэшмапу и смотрим где по ключу массив длинной больше чем 1, выводим первые 2 элемента - пара вершин с одинаковым множеством сыновей(включая вершину).


``` java
package YandexInterview;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

//class TreeNode {
//    char value;
//    TreeNode left, right;
//
//    TreeNode(char value) {
//        this.value = value;
//        left = right = null;
//    }
//}

public class OptimizedEquivalentSubtrees {
    // Хранит побитовые маски для каждой вершины и соответствующие вершины
    private Map<Integer, List<TreeNode>> masksToNodes = new HashMap<>();

    private Pair<TreeNode, TreeNode> findEquivalent(TreeNode root) {
        dfs(root);
        for (List<TreeNode> nodes : masksToNodes.values()) {
            if (nodes.size() > 1) {
                // Нашли эквивалентные вершины
                return new Pair<>(nodes.get(0), nodes.get(1));
            }
        }
        return null; // Если эквивалентные вершины не найдены
    }

    private int dfs(TreeNode node) {
        if (node == null) return 0;

        int mask = 1 << (node.value - 'A');
        int leftMask = dfs(node.left);
        int rightMask = dfs(node.right);

        mask |= leftMask | rightMask;

        masksToNodes.putIfAbsent(mask, new ArrayList<>());
        masksToNodes.get(mask).add(node);

        return mask;
    }

class Pair<T1, T2> {
    T1 first;
    T2 second;

    Pair(T1 first, T2 second) {
        this.first = first;
        this.second = second;
    }
}
    }

```
