# 기사단원의 무기
3개의 인수(number, limit, power)가 주어진다.<br>
#### 1. 1번~number번 까지의 기사단원이 있다.
#### 2. 각 기사단원은 본인이 해당하는 번호의 약수 갯수만큼의 힘을 가진다.<br>
ex 1) 4번 기사단원: 4의 약수 = 1, 2, 4 -> 3<br>
ex 2) 9번 기사단원: 16의 약수 = 1, 2, 4, 8, 16 -> 5<br>

#### 3. 만약 기사단원이 가지고 있는 힘이 limit를 넘어간다면, 해당 기사단원의 <br> 힘은 power로 제한한다.<br>
ex) limit = 4, power = 2<br>
4번 기사단원의 힘 = 3, 9번 기사단원의 힘 = 2

#### 4. 모든 기사단원의 힘을 합친 수를 구해라.
입출력 예<br>
			

|number|limit|power|result|
|:--:|:--:|:--:|:--:|
|5|3|2|10|
|10|3|2|21|

1. number까지의 모든 약수를 구한다.(for문 1~number)
2. 약수의 갯수를 센다.(count)
3. answer+=count
3. 만약 약수의 갯수가 limit를 넘어가면 count 대신 power를 더한다. 
```javascript
function solution(number, limit, power) {
    let answer = 0;
    for(let i = 1; i<=number;i++){
        let count = 0;
        for(let j = 1;j<=i;j++){
            if(i%j===0){
                count++;
            }
        }
        if(count>limit){
            answer+=power;
        }else{
        answer+=count;}
    }
    return answer;
}
```
ERROR 시간초과 발생 <br>
-> 모든 약수를 구한다면 경우의 수가 너무 많아진다.<br>
-> 20의 약수는 (1, 2, 4, 5, 10, 20)<br>
-> 약수가 제곱근(루트20)보다 작다면 count+=2<br>
-> 약수가 제곱근이라면 count+=1<br>
```javascript
function solution(number, limit, power) {
    let answer = 0;
    for(let i = 1; i<=number;i++){
        let count = 0;
        // Modified
        for(let j = 1;j<=Math.sqrt(i);j++){
            if(i%j===0){
                if(j * j === i) count++;
                else count+=2;
            }
        }
        // Modified
        if(count>limit){
            answer+=power;
        }else{
        answer+=count;}
    }
    return answer;
}
```