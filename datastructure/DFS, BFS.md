# DFS, BFS 알고리즘
## 그래프 탐색 알고리즘 : DFS/BFS

- 탐색(Search)이란 많은 양의 데이터 중에서 원하는 데이터를 찾는 과정
- 대표적인 그래프 탐색 알고리즘으로는 DFS와 BFS가 있다.
- DFS/BFS는 코딩 테스트에서 매우 자주 등장하는 유형

## 사전 지식

**스택 자료구조**

- 먼저 들어온 데이터가 나중에 나가는 형식(선입후출)의 자료구조
- 입구와 출구가 동일한 형태로 스택을 시각화할 수 있다.

```java
import java.util.*;

public class Main {
   public static void main(String[] args) {
       Stack<Integer> stack = new Stack<>();
      //삽입(5) - 삽입(2) - 삽입(3) - 삽입(7) - 삭제() - 삽입(1) - 삽입(4) - 삭제()
       stack.push(5);
       stack.push(2);
       stack.push(3);
       stack.push(7);
       stack.pop();
       stack.push(1);
       stack.push(4);
       stack.pop();
       //스택의 최상단 원소부터 출력 
       while(!stack.empty()) {
            System.out.print(stack.peek()+" ");
            stack.pop();
       }
   }
}
//실행결과 1 3 2 5
```

**스택 자료구조**

- 먼저 들어 온 데이터가 먼저 나가는 형식(선입선출)의 자료구조
- 큐는 입구와 출구가 모두 뚫려 있는 터널과 같은 형태로 시각화 할 수 있다.

```java
import java.util.*;

public class Main {
      public static void main(String[] args) {
	 Queue<Integer> queue = new Queue<>();
         //삽입(5) - 삽입(2) - 삽입(3) - 삽입(7) - 삭제() - 삽입(1) - 삽입(4) - 삭제()
	 q.offer(5);
	 q.offer(2);
         q.offer(3);
	 q.offer(7);
	 q.poll();
	 q.offer(1);
	 q.offer(4);
	 q.poll();
         //먼저 들어온 원소를 추출
	 while(!queue.isEmpty()) {
         System.out.print(queue.peek() + " ");
         queue.poll();
         }
     }
}
//실행결과 3 7 1 4
```

### 재귀함수

- 재귀 함수(Recursive Function)란 자기 자신을 다시 호출하는 함수를 의미
- 단순한 형태의 재귀 함수 예제
    - 재귀 함수를 호출합니다 라는 문자열을 무한히 출력
    - 어느 정도 출력하다가 최대 재귀 깊이 초과 메시지가 출력
- 재귀 함수의 종료 조건
    - 재귀 함수를 문제 풀이에서 사용할 때는 재귀 함수의 종료 조건을 반드시 명시
- 종료 조건을 제대로 명시하지 않으면 함수가 무한히 호출될 수 있다.

```java
//종료 조건을 포함하지 않은 예시
public class Main {
    static void recursive_function() {
        System.out.println("재귀 함수를 호출합니다");
        recursive_function();
    }
    public static void main(String[] args) {
        recursive_function();
    }
}

//종료 조건을 포함하는 예시
public class Main {
    static void recursive_function() {
            if(i == 5) return;
            System.out.println("i + "번째 재귀 함수에서 " + (i + 1) + "번째 재귀 함수를 호출합니다");
            recursive_function(i + 1);
            System.out.println(i + "번째 재귀 함수를 종료합니다");
    }
    public static void main(String[] args) {
            recursive_function();
    }
}
```

**팩토리얼 구현 예제**

- n! = 1 × 2 × 3 × ··· × (n - 1) * n
- 수학적으로 0!과 1!의 값은 1이다.

```java
public class Main {
    //반복적으로 구현한 n!
    static int factorial_interative(int n) {
            int result = 1;
            for(int i = 1; i <= n; i++) {
                    result *= i;
            }
            return result;
    }

    //재귀적으로 구현한 n!
    static int factorial_recursive(int n) {
            if(n <= 1) {
                    return 1;
            }
            return n * factorial_recursive(n - 1);
    }
    
    public static void main(String[] args) {
            System.out.println(factorial_interative(5));
            System.out.println(factorial_recursive(5));
    }
}
```

**최대공약수 계산(유클리드 호제법)**

- 두 개의 자연수에 대한 최대공약수를 구하는 대표적인 알고리즘으로는 유클리드 호제법이 있다.
- 유클리드 호제법
    - 두 자연수 A, B에 대하여 (A > B) A를 B로 나눈 나머지를 R이라고 한다.
    - 이때 A와 B의 최대공약수는 B와 R의 최대공약수와 같다.
- 유클리드 호제법의 아이디어를 그대로 재귀 함수로 작성할 수 있다.
    - 예시 : GCD(192, 162)

  | 단계 | A | B |
      | --- | --- | --- |
  | 1 | 192 | 162 |
  | 2 | 162 | 30 |
  | 3 | 30 | 12 |
  | 4 | 12 | 6 |

    ```java
    public class Main {
        static int gcd(int a, int b) {
            if(a % b == 0) {
                return b;
            }	else {
                return gcd(b, a % b);	
            }
        }
        public static void main(String[] args) {
            System.out.print(gcd(192, 168));
        }
    }
    //실행결과 6 
    ```


### 재귀 함수 사용시 유의 사항

- 재귀 함수를 잘 활용하면 복잡한 알고리즘을 간결하게 작성할 수 있다
    - 단, 오히려 다른 사람이 이해하기 어려운 형태의 코드가 될 수도 있으므로 신중히 사용해야 한다.
- 모든 재귀 함수는 반복문을 이용하여 동일한 기능을 구현할 수도 있으므로 신중하게 사용해야 한다.
- 재귀 함수가 반복문보다 유리한 경우도 있고 불리한 경우도 있다.
- 컴퓨터가 함수를 연속적으로 호출하면 컴퓨터 메모리 내부의 스택 프레임에 쌓인다.
    - 그래서 스택을 사용해야 할 때 구현상 스택 라이브러리 대신에 재귀 함수를 이용하는 경우가 많다.


## DFS (Depth-First Search)

- DFS는 깊이 우선 탐색이라고도 부르며 그래프에서 깊은 부분을 우선적으로 탐색하는 알고리즘이다.
- DFS는 스택 자료구조(혹은 재귀 함수)를 이용하며, 구체적인 동작 과정은 다음과 같다.
    1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다.
    2. 스택의 최상단 노드에 방문하지 않은 인접한 노드가 하나라도 있으면 그 노드를 스택에 넣고 방문 처리를 한다. 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
    3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복한다.

(방문 기준) 번호가 낮은 인접 노드부터 : 시작노드 1

![화면 캡처 2023-06-11 230901](https://github.com/GOBUMGYU/SCU-3.2/assets/106207558/0d4447e4-130b-4175-b7df-4cc3291e40a3)

```java
public class Main {
      public static boolean[] visited = new boolean[9];
      public static ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>();
      //DFS 함수 정의
      public static void dfs(int x) {
          //현재 노드를 방문 처리
          visited[x] = true;		
          System.out.print(x + " ");
          //현재 노드와 연결된 다른 노드를 재귀적으로 방문
          for(int i = 0; i < graph.get(x).size(); i++) {
              int y = graph.get(x).get(i);
              if(!visited[y]) dfs(y);
          }
      }

      public static void main(String[] args) {
            //그래프 초기화
            for(int i = 0; i < 9; i++) {
                graph.add(new ArrayList<Integer>());
            }
            
            //그래프 연결 정보 추가
            graph.get(1).add(2);
            graph.get(1).add(3);
            graph.get(1).add(8);
            
            graph.get(2).add(1);
            graph.get(2).add(7);
            
            graph.get(3).add(1);
            graph.get(3).add(4);
            graph.get(3).add(5);
            
            graph.get(4).add(3);
            graph.get(4).add(5);
            
            graph.get(5).add(3);
            graph.get(5).add(4);
            
            graph.get(6).add(7);
            
            graph.get(7).add(6);
            graph.get(7).add(2);
            graph.get(7).add(8);
            
            graph.get(8).add(1);
            graph.get(8).add(7);
            // dfs(1) 호출 
            dfs(1);
      }			
}
//출력 결과 
//1 2 7 6 8 3 4 5
```

## BFS (Breadth-First Search)

- BFS는 너비 우선 탐색이라고 부르며, 그래프에서 가까운 노드부터 우선적으로 탐색하는 알고리즘이다.
- BFS는 큐 자료구조를 이용하며, 구체적인 동작 과정은 다음과 같다.
    1. 탐색 시작 노드를 큐에 삽입하고 방문 처리를 한다.
    2. 큐에서 노드를 꺼낸 뒤에 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고
    3. 더 이상 2번의 과정을 수행할 수 없을 때까지 반복한다.

(방문 기준) 번호가 낮은 인접 노드부터 : 시작노드 1

![화면 캡처 2023-06-11 230901](https://github.com/GOBUMGYU/SCU-3.2/assets/106207558/0d4447e4-130b-4175-b7df-4cc3291e40a3)

```java
public class Main {
      public static boolean[] visited = new boolean[9];
      public static ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>();

      //BFS 함수 정의
      public static void bfs(int start) {
          Queue<Integer> q = new LinkedList<>();
          q.offer(start);
          //현재 노드를 방문 처리
          int x = q.poll();
          
          while(!q.isEmpty()) {
              //큐에서 하나의 원소를 뽑아 출력
              int x = q.poll();
              System.out.print(x + " ");
              //해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
              for(int i = 0; i < graph.get(x).size(); i++) {
                      int y = graph.get(x).get(i);
                  if(!visited[y]) {
                          q.offer(y);
                          visited[y] = true;
                  }
              }
          }
      }
  
      public static void main(String[] args) {
          //그래프 초기화
          for(int i = 0; i < 9; i++) {
                  graph.add(new ArrayList<Integer>());

          }
      
          graph.get(1).add(2);
          graph.get(1).add(3);
          graph.get(1).add(8);
          graph.get(2).add(1);
          graph.get(2).add(7);
          graph.get(3).add(1);
          graph.get(3).add(4);
          graph.get(3).add(5);
          graph.get(4).add(3);
          graph.get(4).add(5);
          graph.get(5).add(3);
          graph.get(5).add(4);
          graph.get(6).add(7);
          graph.get(7).add(2);
          graph.get(7).add(6);
          graph.get(7).add(8);
          graph.get(8).add(1);
          graph.get(8).add(7);

          int startNode = 1;
          bfs(startNode);
    }
}
```