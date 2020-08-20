## Link
[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42748)


<details>
    <summary>문제</summary>
    
## 문제 설명

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
2에서 나온 배열의 3번째 숫자는 5입니다.
배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때,
commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

## 제한 사항
- array의 길이는 1 이상 100 이하입니다.
- array의 각 원소는 1 이상 100 이하입니다.
- commands의 길이는 1 이상 50 이하입니다.
- commands의 각 원소는 길이가 3입니다.

## 입출력 예
|         array         | commands                          | return      | 
| :-------------------: | --------------------------------- | :---------: | 
| [1, 5, 2, 6, 3, 7, 4] | [[2, 5, 3], [4, 4, 1], [1, 7, 3]] |  [5, 6, 3]  | 
			
입출력 예 설명
- [1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다.
- [1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.
- [1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.

### 출처 
[출처](https://neerc.ifmo.ru/subregions/northern.html)

</details>

<details>
    <summary>풀이</summary>
    
## 풀이

```javascript 
  if(commands.length !== commands.filter(command => command.length === 3).length) return;
  return commands
      .map(command =>
          command.map(num => {
            return num - 1;
          })
      )
      .map(command => {
        return array.slice(command[0], command[1]+1).sort((a,b)=>a-b)[[command[2]]]
      });
```    

## 잡담 및 해설 

```javascript 
  if(commands.length !== commands.filter(command => command.length === 3).length) return;
  return commands
      .map(command =>
          command.map(num => {
            return num - 1;
          })
      )
      .map(command => {
        return array.slice(command[0], command[1]+1).sort()[[command[2]]]
      });
```    
- 처음엔 이렇게 적었었는데 sort() 2번째 케이스에서 자꾸 실패하였다. 
> 그래서 찾아보니 sort() 이런식으로 하면 숫자 순으로 정렬이 잘되길래 sort 이 잘되는 줄 알았지만 
> 아스키코드 순으로 정렬되어 숫자의 크기대로 정렬 되지 않는다고 한다.
> 그래서 숫자의 크기대로 정렬되게 sort 를 바꿔주니 잘작동하였다
> 
- 배열순서를 불러오는건 0,1,2,3 식인데 자리수로 이야기하니깐 헷갈려서 실수를 많이했다.
- command[0], command[1] 이런식보단 명시적으로 적어주는게 좋을것 같다. 
</details>    