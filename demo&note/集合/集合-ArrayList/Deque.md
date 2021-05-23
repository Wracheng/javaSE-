#### Queue 队列

> 实现类 ArrayDeque、LinkedList

#### Deque 双端队列接口 是 Queue 的子接口，可以当栈来用

> 实现类 ArrayDeque、LinkedList
> Stack stack = new Stack(); 不建议这么创建使用 Vector 已被 ArrayList 替代

```java
  Deque deque = new LinkedList();
  public class Stack1 {
    public static void main(String[] args) {
        Deque<String> deque = new LinkedList();
        deque.push("盘子1");
        deque.push("盘子2");
        deque.push("盘子3");
        deque.push("盘子4");
        System.out.println(deque);
        System.out.println(deque.peek()); // 看最上层的元素
        System.out.println(deque.size());
        deque.pop();
        System.out.println(deque); // 删除最上层元素
    }
}
```
