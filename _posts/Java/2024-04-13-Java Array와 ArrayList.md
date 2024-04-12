---
layout: post
title: "Java - Array와 ArrayList 출력, 정렬, 변환"
categories: [Java]
tags: [Java]
---

## 출력

1. **배열(Array)** 출력해서 확인하기

   ```java
   import java.util.Arrays;
   //...
   System.out.println(Arrays.toString(array));
   ```

2. **ArrayList** 출력해서 확인하기

   ```java
   import java.util.ArrayList;
   //...
   System.out.println(arrayList);
   ```

## 정렬

1. **배열(Array)** 정렬하기

   - **오름차순**

     ```java
     import java.util.Arrays;
     //...
     Arrays.sort(array);  // 오름차순
     System.out.println(Arrays.toString(array));
     ```

   - **내림차순**

     ```java
     import java.util.Arrays;
     import java.util.Collections;
     //...
     Arrays.sort(array, Collections.reverseOrder());  // 내림차순
     System.out.println(Arrays.toString(array));
     ```

2. **ArrayList** 정렬하기

- **오름차순**

  ```java
  import java.util.ArrayList;
  import java.util.Collections;
  //...
  Collections.sort(list);  // 오름차순
  System.out.println(list);
  ```

  - **내림차순**

  ```java
  import java.util.Arrays;
  import java.util.Collections;
  //...
  Collections.sort(list, Collections.reverseOrder());  // 내림차순
  System.out.println(list);

  Collections.sort(list);
  Collections.reverse(list); // 이렇게 두줄로도 가능
  ```

## ArrayList <-> Array 변환

1. ArrayList → Array 변환하기

   - 노가다로 for문 돌려서 직접 넣기

     ```java
     import java.util.ArrayList;

     public class Main {
        public static void main(String[] args) {

           ArrayList<String> arrayList = new ArrayList<>();
           arrayList.add("사과");
           //...
           String[] array = new String[arrayList.size()];

           for (int i = 0; i < arrayList.size(); i++) {
                 array[i] = arrayList.get(i);
           }
        }
     }
     ```

   - stream API, toArray 사용하기

     ```java
     import java.util.*;
     //...
     int[] answer = list.stream().mapToInt(i -> i).toArray();
     return answer;
     ```
