用 add first 或 add last 这套新的 API 改写 Deque 的代码

Deque<String> deque = new LinkedList<>();
deque.push("a");
deque.push("b");
deque.addFirst("A");
deque.addLast("B");
System.out.println("第一次打印===" + deque);

String str = deque.peekFirst();
System.out.println("peekFirst===" + str);
System.out.println("第二次打印===" + deque);

while (deque.size() > 0) {
    System.out.println("removeFirst==" + deque.removeFirst());
}
输出结果====
第一次打印===[A, b, a, B]
peekFirst===A
第二次打印===[A, b, a, B]
removeFirst==A
removeFirst==b
removeFirst==a
removeFirst==B

分析 Queue 和 Priority Queue 的源码

Queue的源码比较简单：
 Queue<E> extends Collection<E>

Insert(新增）
新增时出现异常会抛异常
IllegalStateException
IllegalStateException
IllegalStateException
IllegalStateException
<td>{@link Queue#add add(e)}</td>
<td>{@link Queue#offer offer(e)}</td>

Remove(删除)
删除时会返回the head
remove时删除也会抛异常：NoSuchElementException
<td>{@link Queue#remove remove()}</td>
// 返回 null
<td>{@link Queue#poll poll()}</td>
Examine(检查)
// 检查element时为空抛异常：NoSuchElementException
<td>{@link Queue#element element()}</td>
// 返回 null
<td>{@link Queue#peek peek()}</td>

Priority Queue的源码分析：
调用add——>>
offer——>>grow(i + 1)——>>Arrays.copyOf(queue, newCapacity)——>>
System.arraycopy （源目标，源目标的下标，copy对象，目标的下标，最小的数组的length）
System.arraycopy(original, 0, copy, 0,Math.min(original.length, newLength))
下面的2个方法其实没有看懂
offer——>>siftUp(i, e)——>>siftUpUsingComparator(k, x)
offer——>>siftUp(i, e)——>>siftUpComparable(k, x)
构造方法：
PriorityQueue(Comparator<? super E> comparator)
比较器
