---

title : "그리디 알고리즘"
layout : single
categories : 
 - jekyll
 - minimal-mistakes
tags :
 - github pages
 - jekyll
 - minimal-mistakes
use_math : false
date : "2020-04-23 23:00"
---

### 문제(출처 : [백준](https://www.acmicpc.net/problem/2217))

---

##### N(1≤N≤100,000)개의 로프가 있다. 이 로프를 이용하여 이런 저런 물체를 들어올릴 수 있다. 각각의 로프는 그 굵기나 길이가 다르기 때문에 들 수 있는 물체의 중량이 서로 다를 수도 있다.

##### 하지만 여러 개의 로프를 병렬로 연결하면 각각의 로프에 걸리는 중량을 나눌 수 있다. k개의 로프를 사용하여 중량이 w인 물체를 들어올릴 때, 각각의 로프에는 모두 고르게 w/k 만큼의 중량이 걸리게 된다.

##### 각 로프들에 대한 정보가 주어졌을 때, 이 로프들을 이용하여 들어올릴 수 있는 물체의 최대 중량을 구해내는 프로그램을 작성하시오. 모든 로프를 사용해야 할 필요는 없으며, 임의로 몇 개의 로프를 골라서 사용해도 된다.

### 입력

---

##### 첫째 줄에 정수 N이 주어진다. 다음 N개의 줄에는 각 로프가 버틸 수 있는 최대 중량이 주어진다. 이 값은 10,000을 넘지 않는 자연수이다.



### 출력

---

##### 첫 째 줄에 답을 출력한다.



### 해석

---

예를 들어 중량을 20 버틸 수 있는 로프 1개가 버틸 수 있는 총 중량은 20이다. 중량 15를 버틸 수 있는 로프와 같이 쓴다고 하면 버틸 수 있는 총 중량은 35가 아닌 30이다. 그 이유는 무게의 중량은 두 로프에 동일하게 적용한다고 가정했기 떄문에 15의 중량을 버틸 수 있는 로프에 15보다 큰 17.5의 중량을 주게되면 로프는 끊어지게 된다. 따라서 n 개 이상의 로프가 버틸 수 있는 최대 중량은

최대중량이 작은 로프 *n이 된다.

### 소스 

---

로프의 중량이 주어지면 중량이 큰 로프순으로 배열을 해준다.

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;
 
public class Main {
 public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int cnt = Integer.parseInt(st.nextToken());
        int arr[] = new int[cnt];
        for(int i=0; i < cnt; i++) {
            st = new StringTokenizer(br.readLine());
            arr[i] = Integer.parseInt(st.nextToken());
        }
        Arrays.sort(arr);
        
        long max = 0;
        for(int i = cnt-1; i >= 0; i--) {
            arr[i] = arr[i] * (cnt-i);
            if(max < arr[i]) max = arr[i];
        }
        System.out.println(max);
    }
}
//출처 : https://pangsblog.tistory.com/21?category=806064
```

